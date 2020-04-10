---
layout: post
title:      "Building relationships in .Net Core"
date:       2020-04-10 17:55:36 +0000
permalink:  building_relationships_in_net_core
---


As I have been learning the backend framework .Net Core, I have had to change my mindset on how to establish a database.  One of the things I discussed in the last post was figuring out code-first database mangagement instead of database first that you would typically use with Rails.  One of the other things is establishing relationships.

With Rails and ActiveRecord, establishing relationships is as simple as adding a foreign-key to the migration and adding a simple relationship statement to the model.  .Net and EF Core take a reverse approach.  Since the migrations and thus database is being established from the model, and not the other way around, we have to establish the relationships in the models, and most importantly in the DBContext.

As I wrote in my last post, the DB context is super important because that is what establishes which models are saved to the database.  When establishing a simple one-many relationship, there is no need to add anything to the DBContext.  What you do is simply add a foreign key, and a model variable to the many side of the relationship like so:

```
    public class Category
    {
        [Key]
        public int CategoryId { get; set; }
        public int Weight { get; set; }

        public int CourseId { get; set; }
        public Course Course { get; set; }

```

then you add a list to the one side of the relationship like so:

```
public ICollection<Category> Categories { get; set; }
```

I have seen many examples that use List instead of ICollection as well.  As I understand it, List is a child of ICollection, but using ICollection is preferred.

The problem that I ran into when establishing these relationships is the concept of cascading.  Sometimes you need a model to have a one to many relationship with multiple "one" classes.  In my case, establishing a gradebook, my assignments had to belong to a class, but they also had to belong to a category.  The default in EF Core is to cascade delete these relationships so if you have more than one of them, you have multiple cascade delete paths and cause an error.  To fix this, you have to establish which one you want to cascade in the DBContext in the modelBuilder section: 
```
    public class AppDbContext : IdentityDbContext<AppUser>
    {
        public AppDbContext(DbContextOptions<AppDbContext> options): base(options)
        {
        }

            public DbSet<Course> Courses { get; set; }
            public DbSet<Assignment> Assignments { get; set; }
            public DbSet<Category> Categories { get; set; }
        protected override void OnModelCreating(ModelBuilder builder)
        {
            base.OnModelCreating(builder);
            builder.Entity<Assignment>()
                .HasOne(p => p.Course)
                .WithMany(p => p.Assignments)
                .HasForeignKey(p => p.CourseId);

            builder.Entity<Assignment>()
                .HasOne(p => p.Category)
                .WithMany(p => p.Assignments)
                .OnDelete(DeleteBehavior.Restrict)
                .IsRequired(false);
            builder.Entity<UsersInCourses>()
                .HasKey(p => new { p.UserID, p.CourseId });
            builder.Entity<AssignmentsForStudents>()
                .HasKey(p => new { p.UserId, p.AssignmentId });

        }
    }

```
The relevant code is the .OnDelete behavior.  Here I had to restrict the delete behavior so if you deleted a category, it wouldn't delete the assignment.  Of course, that means that category also had to be optional.
