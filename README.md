# xTemplate.js

### What is xTemplate.js

xTemplate.js is a rewritten PHP xTemplate class, works nearly same as PHP version. I really don't know if there were another features which I didn't implement, but suits for all of my needs.

Who doesn't know about PHP xTemplate, this is a class simply for templating front end pages and separating designer and developer or view and controller. Frontend developer creates .html (or any extension) files, backend or (nodejs) developer uses the template to generate the resulting page. It is in active development as of June 8, 2019

By the way, this <u>currently</u> suits best to pure javascripters and for those who remembers PHP xtemplate class. Exactly for oldschool people (like me). Works mostly similar as it was in PHP. What I code in the class maybe full of shi*, maybe not. Works unbelievably fast and eases my own work. Who wants to make it cleaner, faster; commitments, additions, deletions, fixes to my code are welcome. I successfully used this class on 3 different projects without problems.

### Features

* String assignment
* Object assignment
* Template File Caching
* global (or window) String and Object automatic assignment (this eases the most of the work)
* Partial parsing of template (you can put list page, edit page into same template file)
* Direct parse output to selector (first) or append to selector (first) (.out function)
* Get the text for assigning to another template (.text function)

### How to use

    // Here is your logic (you pulled users [probably json format] from server,
    // and it is now array of user objects at a variable: users
    var users = [{id: 1, name: "John"},{id: 2, name: "Doe"}];
    var tpl = new xTemplate('tpl/users.html');
    users.forEach(function(user) {
        tpl.assign('user',user);
        tpl.parse('main.list.user');
    });
    tpl.parse('main.list');
    tpl.out('main.list','#content');
