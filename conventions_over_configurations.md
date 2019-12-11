# Conventions over configuration.

A very interesting rails philosophy. This made me cause a production issue.

We have a cronjob rake task runner that runs a job on a regular basis.

I moved a bunch of files that it used from one app into a gem.

The gem was using rails autoloaders.

I placed the file in the wrong directory, sure the file was loaded in the rails console; But, it was not loaded on the rake tasks.

Because of which our rake task complained that it couldn't find the constant.
