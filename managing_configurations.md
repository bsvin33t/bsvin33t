# Managing configurations

When you own multiple apps that use different ways of configurations(config gem and ansible). It is challenging to understand where the variables are set.

We did manage to move everything over to ansible env vars. But unfortunately, we had some hidden configs lying around in our app.

When we decided to merge that app into another, we missed moving the configurations, which caused it to revert to defaults, which was pointing to our staging configuration, because of which we ended up sending close to 8K emails in a matter of minutes.

We ended up fixing up the configuration, pointing our production configuration to the right files, and setting the defaults correct.

### Moral of the story: BE AWARE OF DEFAULT CONFIGURATIONS.

Please feel free to raise an issue if you felt this post needs more information.

Cheers

Vineeth
