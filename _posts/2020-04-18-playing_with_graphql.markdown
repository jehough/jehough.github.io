---
layout: post
title:      "Playing with Graphql"
date:       2020-04-18 17:51:25 +0000
permalink:  playing_with_graphql
---


Recently I have been playing around with a few different technologies to expand my knowledge of Rails and React.  One of the things that was recommended that I try was GraphQL.  This is a program that allows you to send things similar to an api, but it gives you far more control over what you recieve in return.  
One of the biggest problems with an API is that in order to get a specific data set, you have to either get more than you need, or create a new route with the api info that you need.  For example, lets say you have a recipe model that has attributes of ingredients, steps and cook times.  If you wanted just a list of ingredients to make a grocery list, you have two options.  You could take the API that creates a show page, and just take the piece that you need.  The problem with this path is that you have a bunch of data that just isn't necessary.  With a recipe card, that might not be a big deal, but with something more complex, you may be slowing down response time unnecessarily.  The other thing to do is to make another route.  This isn’t a challenging set up, but if you have to make new routes every time you want to get a specific set of results, you end up cluttering up your controllers.
Enter GraphQL.  GraphQL allows you to set query and mutation types that allow you to get and post specific data without having to create new routes.  Setting up graphql is pretty straight forward.  Several tutorials like this one help lay out the step by step process.  The thing that I found the most difficult is understanding the idea of query types.  
When you install GraphQL, several files are created including app/graphql/types/query_type.rb  This is an important file that allows you to set up your query’s.  When you add a query in a sense, it’s like adding a new API generator that is flexible based on the input it receives.  This file is the root of the generator and then you create types that define each model that you want in the generator.

```
module Types
  class QueryType < Types::BaseObject
    # Add root-level fields here.
    # They will be entry points for queries on your schema.



    field :me,
      [Types::UserType],
      null: false,
      description: "Returns a list of users"

    def me
      User.all
    end
  
    field :budgets,
      [Types::BudgetType],
      null: false,
      description: "Returns a list of budgets"

    def budgets
      Budget.all
    end
  end
end
```
The code above shows that I have two fields in my GraphQL json.  “Me” that is set up for all users now, but will soon become the users information once I set up authorization and authentication, and “budgets” which lists out the budgets.  Each one has a type associated with it.  UserType and BudgetType.  This is where you customize what each model returns.  Below is an example of the user type.

```
module Types
  class UserType < Types::BaseObject
    field :id, ID, null: false
    field :email, String, null: false
    field :budgets, [Types::BudgetType], null: false
  end
end
```
Here we see a couple of fields come up, and then I also call on budgets again.  The difference here, is that the budgets that come up will belong specifically to the listed user.  This is a really convenient way to pass data to your front end that is infinitely malleable and easy to use.

