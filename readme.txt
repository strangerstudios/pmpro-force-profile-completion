=== Paid Memberships Pro - Force Profile Completion ===
Contributors: strangerstudios, paidmembershipspro
Tags: paid memberships pro, pmpro, user fields, profile, members
Requires at least: 5.4
Tested up to: 7.1
Requires PHP: 7.4
Stable tag: 1.1.1
License: GPL-3.0+
License URI: https://www.gnu.org/licenses/gpl-3.0.html

Require all members to complete required profile fields before accessing restricted content.

== Description ==

This plugin extends Paid Memberships Pro to enforce completion of required User Fields before members can access restricted content. If a logged-in member with an active membership has unfilled required fields, they are redirected to the Edit Profile page until those fields are completed.

= Features =

* **Redirect on restricted content** — members with incomplete required fields are redirected to the Edit Profile page when they attempt to access any membership-restricted content.
* **Redirect on login** — members are redirected to the Edit Profile page immediately after logging in if required fields are missing.
* **Inline warning message** — a dismissible error notice lists the specific missing fields at the top of the Edit Profile page.
* **Field highlighting** — incomplete required fields are visually highlighted in the profile form.
* **Submit-time validation** — an error is shown if a member tries to save the profile without filling in all required fields.
* **Conditional field support** — fields with `depends` conditions are only enforced when their parent condition is met; hidden fields are never flagged as missing.
* **Performance caching** — incomplete field results are cached per-user for 10 minutes and automatically cleared when the profile is saved or User Fields settings change.

= How It Works =

1. When a logged-in member with an active level visits a membership-restricted page, the plugin checks whether any required User Fields are empty.
2. If required fields are missing, the member is redirected to the PMPro Edit Profile page (the `member_profile_edit` page).
3. The Edit Profile page displays a warning listing the missing fields and highlights the corresponding form inputs.
4. Once the member fills in all required fields and saves, the cache is cleared and they can access restricted content normally.

PMPro pages (account, billing, cancel, etc.) are always accessible so members are never fully locked out of managing their account. The directory and profile pages are intentionally excluded from the bypass so they can still be gated.

== Installation ==

1. Upload the plugin folder to `/wp-content/plugins/` or install via **Plugins > Add New**.
2. Activate the plugin through the **Plugins** menu in WordPress.
3. In Paid Memberships Pro, go to **Memberships > Settings > User Fields** and mark one or more fields as **Required**.
4. Members with an active membership who have not filled in those fields will be redirected to the Edit Profile page on their next login or when they attempt to view restricted content.

No additional configuration is required.

== Frequently Asked Questions ==

= Does this affect non-members or logged-out visitors? =

No. The redirect only applies to logged-in users who have an active membership level. Logged-out visitors and users without a membership level are handled by PMPro core as normal.

= Which pages can members always access? =

All PMPro-assigned pages (account, billing, cancel, checkout, confirmation, etc.) are always accessible. This prevents members from being fully locked out while they complete their profile. The directory and profile pages are excluded from this bypass so they can remain gated if needed.

= What counts as a "required" field? =

Any field defined through **PMPro > Settings > User Fields** that has the **Required** checkbox enabled. Fields with conditional visibility (`depends`) are only required when their parent field's condition is satisfied.

= Does this work with conditional/dependent fields? =

Yes. If a field is set to only display when another field has a specific value, this plugin checks whether that condition is met before treating the field as required. Fields whose conditions are not satisfied are skipped.

= Will members lose access to their account or billing pages? =

No. PMPro core pages (account, checkout, billing, cancel, etc.) are always reachable so members can still manage their subscription while they complete their profile.

= When is the incomplete-fields cache cleared? =

The cache is cleared automatically when:

* The member saves their profile (`pmpro_personal_options_update` or `profile_update`).
* An admin saves, updates, or deletes the User Fields settings (`pmpro_user_fields_settings` option changes).

The cache has a maximum lifetime of 10 minutes.

== Changelog ==

= 1.1.1 - 2026-09-29 =
* SECURITY: Improved sanitization and escaping throughout the plugin to resolve Plugin Check security findings. #3 (@dparker1005)

= 1.1 - 2026-07-02 =
* BUG FIX: Fixes an issue where it would cause the Member Profile page for the Member Directory and Profile Add On would be 404.

= 1.0 - 2026-04-02 =
* Initial release.
