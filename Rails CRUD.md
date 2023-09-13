# Rails CRUD Operations

## Table of Content

1) Introduction

2) Setting up the Rails Application

3) Creating a Model

4) Generating Controllers

5) Routes

6) Create - Adding Records

7) Read - Retrieving Records

8) Update - Modifying Records

9) Delete - Removing Records

## Introduction

CRUD operations are fundamental to any web application. They stand for Create, Read, Update, and Delete, representing the four basic functions for persistent storage. Ruby on Rails makes it easy to implement these operations in your web application.


In this comprehensive guide, we will walk through each CRUD operation step-by-step in a Rails application.

## Setting up the Rails Application

Before diving into CRUD operations, let's set up a new Rails application if you haven't already. Open your terminal and run:

    rails new my_app
    cd my_app

This command will create a new Rails application named my_app. Navigate to the application folder with cd my_app.

## Creating a Model

A model represents the data structure of your application. For this example, let's create a model called Task to manage tasks. Use the following command:

    rails generate model Task title:string description:text

This command generates a Task model with title (string) and description (text) fields. Now, migrate the database to apply these changes:

    rails db:migrate

## Generating Controllers

Next, we'll generate a controller to handle CRUD operations for our Task model. Run the following command to create a controller named Tasks:

    rails generate controller Tasks

This command generates the tasks_controller.rb file in the app/controllers directory.

## Routes

To define routes for our CRUD operations, open the config/routes.rb file and add the following code:

    Rails.application.routes.draw do
    resources :tasks
    root 'tasks#index'
    end
    
This code sets up RESTful routes for the Task model, including index, new, create, edit, update, and destroy actions.

## Create - Adding Records
### Create Action (Controller)

In the app/controllers/tasks_controller.rb, add the following code to handle the creation of tasks:

    def new
      @task = Task.new
    end

    def create
      @task = Task.new(task_params)
      if @task.save
        redirect_to tasks_path
      else
        render 'new'
      end
    end

    private

    def task_params
      params.require(:task).permit(:title, :description)
    end

The new action displays the form to create a new task, and the create action handles form submission, creating a new task in the database.

### Create View (HTML Form)

Create a view file named new.html.erb in the app/views/tasks directory. This file should contain a form for creating tasks.

    <%= form_for @task do |f| %>
      <div class="field">
        <%= f.label :title %>
        <%= f.text_field :title %>
      </div>

      <div class="field">
        <%= f.label :description %>
        <%= f.text_area :description %>
      </div>

      <div class="actions">
        <%= f.submit 'Create Task' %>
      </div>
    <% end %>

### Create Route

No additional routes are needed for the create action since it's handled by the resources declaration in config/routes.rb.
