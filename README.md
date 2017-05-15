# Vending Machine

[Live](all-aboard-vending-machine.herokuapp.com)

## Overview

__Vending Machine__ is a basic interface that demonstrates [All Aboard](https://github.com/tomerovadia/AllAboard), a light-weight web application framework.

It renders a collection of items, each including a name, image, price and id.

Users can interact with the vending machine as a customer (default) or operator. A button at the top allows them to toggle between roles.

Operators can add or remove items. Customers can purchase items.

This app persists data using a cookie stored in the user's browser. This utilizes the `sesssion` functionality provided by All Aboard. Items as well as mode (`customer` or `operator`) are persisted.

## Controllers

Vending Machine manages two resources: `Vending Machine`s and `Item`s. Only one `Vending Machine` is instantiated per session of the app, and this instance stores multiple instances of `Items`. The app has a `VendingMachineController` and `ItemsController` to handle HTTP requests regarding these resources.

## Routes

Vending Machine utilizes four routes (declared in `routes.rb`):

  * `get Regexp.new("^/$"), VendingMachinesController, :show`
    * Renders the vending machine homepage
    * Called when visiting the root path
  * `delete Regexp.new("^/vending-machines$"), VendingMachinesController, :destroy`
    * sets the `session` cookie to `nil`, thus reseting the vending machine to its default state
    * called by the `Reset` button
  *  `post Regexp.new("^/items$"), ItemsController, :create`
    * Creates a new item
    * Called by the add items form available while in operator mode
  * `delete Regexp.new("^/items/(?<id>.+)$"), ItemsController, :destroy`
    * Removes an item
    * Called by either the `Purchase` button (customer mode) or `Remove` button (operator mode)
