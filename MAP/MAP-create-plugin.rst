.. _MAP-create-plugin:

===========
MAP Plugins
===========

The Plugin lies at the heart of the MAP framework.  The key idea behind the plugins is to make them as simple as possible to implement.  The interface is defined in documentation and the plugin developer is expected to adhere to it.  The framework leaves the responsibility of conforming to the plugin interface up to the plugin developer.  The plugin framework is based on Marty Alchin[1] article on a plugin framework for Django.  It is very lightweight and requires no external libraries and can be made to work with Python 2 and Python 3 simultaneously.


MAP Step
========

The MAP Step is the plugin developers need to work from






Ports
=====

One port can either use or provide one thing. A single port should not both provide a thing and use a thing.  Ports are ordered by position.



References
==========

[1] http://martyalchin.com/2008/jan/10/simple-plugin-framework/ Marty Alchin on January 10, 2008