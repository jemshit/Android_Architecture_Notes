# Differences

![Differences](https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/mvc_mvp_mvvm.png)
[[1]](#references)

"**MVC – Model View Controller**
Let’s look at MVC first. You’ll notice a few things about the diagram:

The input is directed at the Controller first, not the view. That input might be coming from a user interacting with a page, but it could also be from simply entering a specific url into a browser. In either case, its a Controller that is interfaced with to kick off some functionality.

There is a many-to-one relationship between the Controller and the View. That’s because a single controller may select different views to be rendered based on the operation being executed.

Note the one way arrow from Controller to View. This is because the View doesn’t have any knowledge of or reference to the controller.

The Controller does pass back the Model, so there is knowledge between the View and the expected Model being passed into it, but not the Controller serving it up.

**MVP – Model View Presenter**
Now let’s look at the MVP pattern. It looks very similar to MVC, except for some key distinctions:

The input begins with the View, not the Presenter.

There is a one-to-one mapping between the View and the associated Presenter.

The View holds a reference to the Presenter. The Presenter is also reacting to events being triggered from the View, so its aware of the View its associated with.

The Presenter updates the View based on the requested actions it performs on the Model, but the View is not Model aware.

**MVVM – Model View View Model**
So with the MVC and MVP patterns in front of us, let’s look at the MVVM pattern and see what differences it holds:

The input begins with the View, not the View Model.

While the View holds a reference to the View Model, the View Model has no information about the View. This is why its possible to have a one-to-many mapping between various Views and one View Model…even across technologies. For example, a WPF View and a Silverlight View *could* share the same View Model. However, my own feeling is that this is a bad practice and creates Franken-ViewModels that have too many responsibilities. It’s better to keep it as a one-to-one mapping instead.

You’ll also notice that the View has no idea about the Model in the MVVM pattern. This is because, as far as the View knows, its “Model” IS the View Model (hence its name). Because of how data-binding and other features like commanding work in WPF and Silverlight, there is rich communication between the View and View Model, isolating the View from having to know anything about what’s really happening behind the scenes." [[1]](#references)

- "Let me explain what I mean in the diagram. When you first try to access an MVC application, you would type something like this:

www.somewebsite.com/customers

When that request comes in, the MVC routing engine determines which controller "customers" refers to and directs it to the proper or default method. Its within that method where its determined what view should be rendered.

Let's say you clicked a link on the rendered view to www.somewebsite.com/customerlist. Same thing happens - the routing engine determins which controller "customerlist" is referring to and that controller determines which view gets rendered.

That's one of the biggest diferences between MVC and traditional ASP.NET webform apps - you're not navigating to the location of a page in a folder structure, you're passing a request to a controller that determines what gets rendered...  The view knows information about what model its being passed for binding purposes. However, the view *doesn't* know how to get the model or what context the model is in as far as state. It only knows that it can expect a Customer object, for example, and it has helpers to bind properties of the customer to itself." [[1]](#references)


### References

[1] "MVVM Compared To MVC and MVP," 21 11 2009. [Online]. Available: https://web.archive.org/web/20170829105757/http://geekswithblogs.net/dlussier/archive/2009/11/21/136454.aspx. [Accessed 03 03 2018].


---
Last Edited: 03.03.2018
