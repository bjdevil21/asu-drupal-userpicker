DESCRIPTION
--------------------------
Provides a custom user field widget for picking users in Drupal and ASU LDAP,
and creating those not yet in Drupal.

INSTALLATION
--------------------------
Install the module as usual, see http://drupal.org/node/70151 for further
information.

Configuration
--------------------------
The ASU Userpicker module creates an AJAX autoocomplete userpicker widget
and is easily assignable using the Fields managment UI in Drupal.

It requires the CAS Attributes, LDAP Servers and User Reference modules to
be enabled, and at least one LDAP Server to be configured.

Using the ASU Userpicker with non-Field API managed fields requires custom
code to map it into place:

Implement a form_alter() to change an existing userpicker field's
'#autocomplete_path' to 'autocomplete/asu/user' and the '#element_validate'
field to 'asu_userpicker_autocomplete_validate'.

Like so:
$form['my_picker_field']['#autocomplete_path'] = 'autocomplete/asu/user';
$form['my_picker_field']['#element_validate'] = 'asu_userpicker_autocomplete_validate';

Additional configurations for the module can be made using the devel/php tool,
as there is no admin UI for these ASU Userpicker variables:

// LDAP server configuration machine name to use if not using default setup at
// install.
variable_set('asu_userpicker_ldap_server', 'your_server_machinename');

// List of roles to use in filtering user results.
variable_set('asu_userpicker_referenceable_roles', 
    serialize(array(
      2 => '2', // Authenticated user
      3 => '0',
    )));

// List of statuses to use in filtering user results.
variable_set('asu_userpicker_referenceable_status', 
    serialize(array(
      1 => '1', // Active users
      0 => '0',
    )));

// A view to use in selecting users.
variable_set('asu_userpicker_referenceables_view', 'your_view_name');

// Userpicker label for CAS Add User
variable_set('asu_userpicker_label', 'USER');

// Local user search fields
// Fields available are any fields attached to the user object.
variable_set('asu_userpicker_search_user_fields', array('field_first_name', 'field_last_name', 'another_field_machine_name'));

// LDAP user search fields/filters
// Filters available include: cn (full name), sn (last name), givenname (first name), asuriteid, mail (email), eid, primaryaffiliation, department, departmentcode
variable_get('asu_userpicker_search_ldap_filters', array('asuriteid', 'cn', 'mail'));

PERMISSIONS
--------------------------

PAGES
--------------------------

TABLES
--------------------------

BLOCKS
--------------------------
None.

HOOKS
--------------------------
See the API file...  [ TODO ]

CREDITS
--------------------------
ASU Userpicker was created by Michael Samuelson <mlsamuel@asu.edu> /
<mlsamuelson@gmail.com> (http://mlsamuelson.com).


