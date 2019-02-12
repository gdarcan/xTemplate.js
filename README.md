# xTemplate.js

*source code is coming soon*

## What is xTemplate.js

xTemplate.js is a rewritten PHP xTemplate class (read 3rd paragraph), works nearly same as PHP version. I really don't know if there were another features which I didn't implement, but suits for all of my needs and I hope it also suits your needs. Works very well on single page web apps, hybrid mobile apps, PWA's or anywhere you want.

Code is not-state-of-the-art piece and I have a feeling that it works fast enough. I didn't make any benchmarking. Also it works at backend nodejs or fronted. Uses fs at node and xhr at frontend. Doesn't work asynchronously to read/download template file so, if you have a large template file, better to read at start/onload and have it cached to respond faster to requests.

BTW, who doesn't know about PHP xTemplate, this is a class simply for templating front end pages and separating designer and developer or view and controller. Frontend developer creates .html (or any extension) files, backend or (nodejs) developer or frontend javascript developer uses that template to generate the resulting page. xTemplate.sj is in active development as of February 13, 2019.

If you wanna contribute to make it cleaner, faster, more compatible etc... you're welcome.

## Features

* String assignment
* Object assignment //TODO recursion inside object's objects
* Template File Caching (not to read the same file again till restart/reload)
* global (or window) String and Object automatic assignment (this eases the most of the work)
* Partial parsing of template (you can put list page, edit page into same template file)
* Direct parse output to selector (first) or append to selector (first) (.out function)
* Get the text for assigning to another template (.text function)

## How to use

### General Usage Scenario

**tpl/users.html**

    <!-- BEGIN: main -->
    
        <!-- BEGIN: list -->
            <h2>{page_title}</h2>
            <table>
                <thead>
                    <tr>
                        <td>ID</td>
                        <td>{str._USERNAME}</td>
                        <td>{str._CITY}</td>
                    </tr>
                </thead>
                <tbody>
                    <!-- BEGIN: user -->
                    <tr>
                        <td>{userObj.id}</td>
                        <td>{userObj.name}</td>
                        <td>{userObj.city}</td>
                    </tr>
                    <!-- END: user -->
                </tbody>
            </table>
        <!-- END: list -->

        <!-- BEGIN: add_edit -->
        Here is your add/edit form
        <!-- END: add_edit -->
    
    <!-- END: main -->

**someFrontendJavascript.js** (Don't use this name, use whatever else you want)

    // You have a window object named str which includes your language specific
    // strings and changes with active language, something like below
    var str = {
        _USERNAME: "Username",
        _CITY: "City",
    }
    // Here comes your logic:
    // You pull users (probably json format) from server,
    // and now it is an array of user objects like below
    var users = [
        {
            id: 1,
            name: "John",
            city: "New York",
        },
        {
            id: 2,
            name: "Doe"
            city: "Paris"
        }
    ];
    var tpl = new xTemplate('tpl/users.html');
    tpl.assign('page_title','Users Page');
    users.forEach(function(user) {
        tpl.assign('userObj', user);
        tpl.parse('main.list.user');
    });
    tpl.parse('main.list');
    tpl.out('main.list','#content');

DOM originally

    <!-- HTML stuff here head body etc. -->
    <div id="content"></div>
    <script src="someFrontendJavascript.js></script>
    <!-- closing of body html etc and your other stuff -->

DOM after script run

    <!-- HTML stuff here head body etc. -->
    <div id="content">
        <h2>Users Page</h2>
        <table>
            <thead>
                <tr>
                    <td>ID</td>
                    <td>Username</td>
                    <td>City</td>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>1</td>
                    <td>John</td>
                    <td>New York</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>Doe</td>
                    <td>Paris</td>
                </tr>
            </tbody>
        </table>
    </div>
    <script src="someFrontendJavascript.js></script>
    <!-- closing of body html etc and your other stuff -->
