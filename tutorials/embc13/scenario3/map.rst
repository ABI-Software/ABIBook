.. _embc13-scenario3-map:

Wrapping your favorite tool as a MAP client plugin
==================================================

The MAP framework is a very general purpose workflow-based tool. By taking advantage of the collaborative development and sharing features of the Physiome Model Repository, you have seen in the previous :ref:`MAP tutorial <embc13-MAP-import-tutorial>` how it is possible to share your work in a manner that makes it easy for other scientists to utilise and extend.

With the plugin approach used by the MAP client software, it is possible to wrap you favorite software tools to make them available as steps in a MAP workflow. For example, the previous tutorials have made use of the :ref:`Zinc <MAP-install-zinc>` visualisation and field manipulation library.

The process of developing a MAP plugin is beyond the scope of this tutorial. If you are interested, there is the beginnings of some :ref:`documentation <MAP-tutorial-plugin>` for this process which will be developing in the near future. There is also a skeleton plugin that comes the MAP client software (in the ``plugins`` folder) which serves as the starting point for developing any new plugin and the `github project`_ which will contain a collection of MAP plugins. If you are interested in developing a plugin or would like help wrapping your favorite tool as a workflow step, please don't hesitate to contact the `MAP team <https://launchpad.net/mapclient>`_ (or talk to Hugh today!).

.. _github project: https://github.com/mapclient-plugins