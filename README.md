# Foo

using ember-cli and getting started using generators

## Get set up

First things first, you need to have ember-cli installed: `npm install -g ember-cli`. Once you have that you can create a new project with the command `ember new foo`, which will create the _foo_ application structure.

We don't need ember-data at this point, so let's get rid of it and the csp which throws some warnings that we don't need to worry about for this project:
```
bower uninstall --save ember-data && npm uninstall --save-dev ember-data ember-cli-content-security-policy
```

We also want to use the [pods](http://www.ember-cli.com/#using-pods) project folder structure to keep things organized a bit better. To do this, follow these steps:
* go into the `app/` directory and delete all of the folders except for `styles`
* edit the `.ember-cli` file and add this line: `"usePods": true`
* in `config/environment.js` add `podModulePrefix: 'foo/pods'` _note: the 'foo' part of this path should be the `modulePrefix` value_
* edit `app/app.js` and add `podModulePrefix: config.podModulePrefix`

Now we are all set to go.

## Running / Development

* `ember server`
* Visit your app at [http://localhost:4200](http://localhost:4200).

### Code Generators

Make use of the many generators for code, try `ember help generate` for more details

#### Generate the Application

* Start by creating an application template with `ember g template application` this will create the template that is always rendered for every "page," essentially this is our wrapper. To get any substates/pages to load, we need to add an `{{outlet}}` to this template file.
* Create an index template which will be our "homepage" with `ember g template index`
* In the application template, add some navigation using the `{{link-to}}` helper:
```
<header>
  <h1>FOO</h1>
  <nav>
    <ul>
      <li>{{link-to 'Home' 'index'}}</li>
      <li>{{link-to 'About' 'about'}}</li>
    </ul>
  </nav>
</header>
```
* Since we are trying to link to the "about" route, we need to create it with `ember g route about`. This command will generate our route javascript file as well as a template file. We can add content to the `about/template.hbs` file accordingly. This generate command also registered and added the route to the `router.js` file, making it accessible to our application.
* You should now be able to click on the navigation links and see the content change between the "homepage" and the "about page"

#### Refactor Redundancy
You can see that we created two navigation items, but if we want to make this a little better, we should use [components](http://guides.emberjs.com/v1.11.0/components/).

Let's generate a nav item component with `ember g component nav-item`, add our template code `{{link-to title route}}` which will bind the `title` and `route` to properties set on the component. We also need to tell the component what HTML tag it should be instead of the default `<div>`. In the `nav-item/component.js` file, add the property `tagName: 'li'` and now refactor the application template to use our new component.
```
<header>
  <h1>FOO</h1>
  <nav>
    <ul>
      {{nav-item title="Home" route="index"}}
      {{nav-item title="About" route="about"}}
    </ul>
  </nav>
</header>
```

Everything should work as before, but look a little better.


### Running Tests

* `ember test`
* `ember test --server`

### Building

* `ember build` (development)
* `ember build --environment production` (production)

### Deploying

Specify what it takes to deploy your app.

## Further Reading / Useful Links

* [ember.js](http://emberjs.com/)
* [ember-cli](http://www.ember-cli.com/)
* [ember community slack](https://ember-community-slackin.herokuapp.com/)
* [ember observer - a place to find addons](http://emberobserver.com/)
* Development Browser Extensions
  * [ember inspector for chrome](https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi)
  * [ember inspector for firefox](https://addons.mozilla.org/en-US/firefox/addon/ember-inspector/)
