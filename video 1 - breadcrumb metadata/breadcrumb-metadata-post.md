#Adding Breadcrumb metadata to your website

I have created a video explaining how you can add breadcrumb metadata to your Drupal 8 website. It quickly explains how to add the metadata to your theme and how you test the results.

If you don't need the explanations and details, feel free to just copy the code below.

You will need a twig template in your theme that overwrites the standard breadcrumb twig template. The name has to be "breadcrumb.html.twig".

Creating the file you can use the following code to have the metadata included in the Microdata format.

```twig
{#
/**
 * @file
 * Theme override for a breadcrumb trail.
 *
 * Available variables:
 * - breadcrumb: Breadcrumb trail items.
 */
#}
{% if breadcrumb %}
  <nav class="breadcrumb" role="navigation" aria-labelledby="system-breadcrumb">
    <ol itemscope itemtype="http://schema.org/BreadcrumbList">
    {% for item in breadcrumb %}
      <li itemprop="itemListElement" itemscope itemtype="http://schema.org/ListItem">
        {% if item.url %}
          <a itemscope itemtype="http://schema.org/Thing" itemprop="item" href="{{ item.url }}">
            <span itemprop="name">{{ item.text }}</span>
          </a>
        {% else %}
          <span itemprop="name">{{ item.text }}</span>
        {% endif %}
        <meta itemprop="position" content="{{ loop.index }}" />
      </li>
    {% endfor %}
    </ol>
  </nav>
{% endif %}
```

Make sure to test your changes in Google's structured data testing tool: 

https://search.google.com/structured-data/testing-tool

More information regarding breadcrumb metadata can be found on 

https://developers.google.com/search/docs/data-types/breadcrumbs

