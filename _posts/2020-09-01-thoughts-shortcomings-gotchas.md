---
layout: post
title:  "Thoughts, shortcomings, gotchas on SPFx Dynamic Data capabilities"
author: Arjun Menon
categories: [ PnPPowerShell, SharePoint ]
image: assets/images/post-1.jpg
tags: [PnPPowerShell]
---

It’s the festive break, and I thought I’d try the new Dynamic Data capabilities that recently went to General Availability in SharePoint Framework 1.7.

I’ve been building a lot of React components lately, and all the SPFx web parts and application customisers with visual elements we create at Engage Squared, are built on React.  Dynamic Data in SPFx introduces a whole new world of modularity that we haven’t had before. We can now split up the page elements into multiple web parts that, in the past, have been combined as one web part so state can be passed between them.  Doing this gives control back to the page author, with the ability to position components how they wish.

Breaking components up in to individual web parts also changes the way the components are designed, and forces the developer to leverage the responsive capabilities of modern pages.  Modern pages are designed from the ground up to work on many different screen sizes, and as long as each individual component respects responsive design, we can let the modern page infrastructure do the rest.

## SPFx Dynamic Data: Gotcha and Shortcoming

It’s somewhat disappointing to note that Dynamic Data in SPFx is not supported on classic pages.  As of the day I published this post, when you introduce a component that calls the

{% highlight typescript %}
context.dynamicDataSourceManager.initializeSource()
{% endhighlight %}


With that shortcoming aside, I found adding dynamic data capabilities to be relatively light-weight, and also flexible enough to use in any number of scenarios (more on that later).

One gotcha I discovered that had me tearing my hair out for a good day or two (in between festive partying, dinner, drinking, and pudding) was when I encountered the following

{% highlight typescript %}
Serialization failed for web part WebPart.DynamicDataConsumerWebPart.3c797b3b-6634-404c-8772-d09a49f94236
exception:

Uncaught Error: Serialization failed for web part WebPart.DynamicDataConsumerWebPart.3c797b3b-6634-404c-8772-d09a49f94236.
    at t [as constructor] (sp-pages-assembly_en-us_c565a80043b8eecd7e332455be57225f.js:857)
    at new t (sp-pages-assembly_en-us_c565a80043b8eecd7e332455be57225f.js:1445)
    at Function.t.create (sp-pages-assembly_en-us_c565a80043b8eecd7e332455be57225f.js:1445)
    at DynamicDataConsumerWebPart.t._internalSerialize (sp-pages-assembly_en-us_c565a80043b8eecd7e332455be57225f.js:1445)
    at DynamicDataConsumerWebPart.t._internalSetDirtyBit (sp-pages-assembly_en-us_c565a80043b8eecd7e332455be57225f.js:1445)
    at sp-pages-assembly_en-us_c565a80043b8eecd7e332455be57225f.js:1445
    at sp-pages-assembly_en-us_c565a80043b8eecd7e332455be57225f.js:1445
    at Map.forEach (<anonymous>)
    at e._executeForIdsOrAll (sp-pages-assembly_en-us_c565a80043b8eecd7e332455be57225f.js:1445)
    at sp-pages-assembly_en-us_c565a80043b8eecd7e332455be57225f.js:1445
{% endhighlight %}

Don’t panic.

This happens when dynamic data properties are added to a web part’s propertiesMetadata() readonly call, and have not been added to the properties node of the web part’s *.manifest.json file. When your*WebPart.ts file has propertiesMetadata() like this:

{% highlight typescript %}
export default class DynamicDataConsumerWebPart extends BaseClientSideWebPart<IDynamicDataConsumerWebPartProps> {

  protected get propertiesMetadata(): IWebPartPropertiesMetadata {
    return {
      'dynamicProperty0': { dynamicPropertyType: 'string' }
    };
  }

  public render(): void {
  
    // Removed for brevity

    ReactDom.render(element, this.domElement);
  }

  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {

    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
          primaryGroup: {
          groupFields: [
            PropertyPaneTextField('dynamicProperty0', {
              label: strings.PropertyLabelDynamicProperty0
            })
          ]

        },
        secondaryGroup: {
          groupFields: [
          PropertyPaneDynamicFieldSet({
            label: strings.PropertyLabelFieldSetDynamicProperty0,
            fields: [
              PropertyPaneDynamicField('dynamicProperty0', {
                label: strings.PropertyLabelDynamicProperty0
              })
            ],
            sharedConfiguration: {
              depth: DynamicDataSharedDepth.Property
            }
          })
        ]
        },
        showSecondaryGroup: !!this.properties.dynamicProperty0.tryGetSource()
      }
    ]
  };
  
}
{% endhighlight %}
… the web part’s manifest file should include “dyanmicProperty0” in the “properties” node:

After adding them to your web part’s .manifest.json file, you will need to redeploy the app’s sppkg file to the app catalog, and you will also need to remove and re-add the web part to the page you’re working on.

This is a departure from the implementation of other web part properties types. SPFx web part properties have not been required in the .manifest.json file in the past.  I was wondering if the product team will consider this inconsistency to be a bug, so I raised this issue in the sp-dev-docs repo, found here.