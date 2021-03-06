# WSU People Directory

[![Build Status](https://travis-ci.org/washingtonstateuniversity/WSU-People-Directory.svg?branch=master)](https://travis-ci.org/washingtonstateuniversity/WSU-People-Directory)

A WordPress plugin to maintain a central directory of people.

## Hooks

WSU People is configured by default to work on Washington State University's WordPress platform. However, several hooks are included that can be used to adapt the plugin so that it works in other setups.

### A dual purpose plugin

In its full capacity, the WSU People Directory plugin is activated globally on a multi-network/multisite WordPress installation. These hooks exist to differentiate between the main site that maintains a record of people and other sites that pull these records from a central source.

The `wsuwp_people_is_main_site` filter is available for indicating that a site is the main people directory. By default, this filter is `false` and the plugin assumes the role of a secondary site.

### REST API

The `wsu_people_directory_rest_url` filter is available to modify the default REST URL used for people records. This is attached to `people.wsu.edu` by default, but can be used with any WordPress installation.

Once a site has been designated as the main people directory using the `wsuwp_people_is_main_site` filter, the `wsuwp_people_directory_rest_url` should be updated to match that site's settings.

### Organization Data

The `wsuwp_people_get_organization_person_data` filter is available for providing organizational data about a person. This allows for the automatic collection of basic data that should be managed through active directory or some other means.

A specific return structure is expected. Data will be sanitized after retrieval:

```php
$return_data = array(
    'given_name' => '',
    'surname' => '',
    'title' => '',
    'office' => '',
    'street_address' => '',
    'telephone_number' => '',
    'email' => '',
);
```

## REST API

WSU's directory of people can best be consumed via the [WordPress REST API](http://v2.wp-api.org/):

* `https://people.wsu.edu/wp-json/wp/v2/people`

The general [documentation](http://v2.wp-api.org/) for the REST API is the best place to see how to interact with the API itself. We provide several custom fields with person records returned by the API.

Here is an raw overview of the properties attached to each object:

```
{
"id": 21,
"date": "2015-07-10T09:47:50",
"date_gmt": "2015-07-10T16:47:50",
"guid": {
  "rendered": "https://people.wsu.edu/?post_type=wsuwp_people_profile&#038;p=21"
},
"modified": "2015-11-23T16:49:52",
"modified_gmt": "2015-11-24T00:49:52",
"slug": "jeremy-felt",
"type": "wsuwp_people_profile",
"link": "https://people.wsu.edu/profile/jeremy-felt/",
"title": {
  "rendered": "Jeremy Felt"
},
"content": {
  "rendered": "<p>This is my official biography text.</p>\n"
},
"author": 1,
"featured_image": 32,
"first_name": "Jeremy",
"last_name": "Felt",
"position_title": "SR WORDPRESS ENGR, UCOMM",
"office": "INFO TECH 2008",
"address": "P O BOX 641227",
"phone": "509-335-5301",
"phone_ext": "",
"email": "jeremy.felt@wsu.edu",
"office_alt": "ITB 2008 Howdy",
"phone_alt": "",
"email_alt": "",
"website": "",
"bio_college": "<p>Testing out my college level biography</p>\n",
"bio_lab": "<p>Testing out my lab level biography</p>\n",
"bio_department": "<p>Testing out my department level biography</p>\n",
"cv_employment": "<p>Testing employment</p>\n",
"cv_honors": "<p>Testing honors and awards</p>\n",
"cv_grants": "<p>Testing grants, contracts</p>\n",
"cv_publications": "<p>Testing publications</p>\n",
"cv_presentations": "<p>Testing presentations</p>\n",
"cv_teaching": "<p>Testing instruction</p>\n",
"cv_service": "<p>Testing professional service</p>\n",
"cv_responsibilities": "<p>Testing responsibilities</p>\n",
"cv_affiliations": "<p>Testing affiliations</p>\n",
"cv_experience": "<p>Testing prof development</p>\n",
"working_titles": [],
"degrees": [],
"cv_attachment": "",
"profile_photo": "",
"_links": {
  "self": [
	{
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/people/21"
	}
  ],
  "collection": [
	{
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/people"
	}
  ],
  "author": [
	{
	  "embeddable": true,
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/users/1"
	}
  ],
  "version-history": [
	{
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/people/21/revisions"
	}
  ],
  "http://api.w.org/featuredmedia": [
	{
	  "embeddable": true,
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/media/32"
	}
  ],
  "http://api.w.org/attachment": [
	{
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/media?post_parent=21"
	}
  ],
  "http://api.w.org/term": [
	{
	  "taxonomy": "post_tag",
	  "embeddable": true,
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/people/21/terms/tag"
	},
	{
	  "taxonomy": "wsuwp_university_category",
	  "embeddable": true,
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/people/21/terms/wsuwp_university_category"
	},
	{
	  "taxonomy": "wsuwp_university_location",
	  "embeddable": true,
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/people/21/terms/wsuwp_university_location"
	},
	{
	  "taxonomy": "wsuwp_university_org",
	  "embeddable": true,
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/people/21/terms/wsuwp_university_org"
	},
	{
	  "taxonomy": "appointment",
	  "embeddable": true,
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/people/21/terms/appointment"
	},
	{
	  "taxonomy": "classification",
	  "embeddable": true,
	  "href": "http://dev.people.wsu.edu/wp-json/wp/v2/people/21/terms/classification"
	}
  ]
}
}
```
