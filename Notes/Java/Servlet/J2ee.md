If it needs to remove the servlet, the container finalizes the servlet by calling the servlet’s `destroy` method. For more information, see [Finalizing a Servlet](https://javaee.github.io/tutorial/servlets010.html#BNAGS).

### Handling Servlet Lifecycle Events

You can monitor and react to events in a servlet’s lifecycle by defining listener objects whose methods get invoked when lifecycle events occur. To use these listener objects, you must define and specify the listener class.

#### Defining the Listener Class

You define a listener class as an implementation of a listener interface. [Table 18-1](https://javaee.github.io/tutorial/servlets002.html#BNAFL) lists the events that can be monitored and the corresponding interface that must be implemented

Use the `@WebListener` annotation to define a listener to get events for various operations on the particular web application context. Classes annotated with `@WebListener` must implement one of the following interfaces: