Ardent's Changelog
==================

## Laravel 6+ Compatibility Update

### Changed
- Updated all Illuminate package dependencies from `~5.0` to `^6.0|^7.0|^8.0|^9.0|^10.0` for Laravel 6+ compatibility
- Replaced deprecated `Input::` facade with `request()` helper function
- Replaced deprecated `snake_case()` helper with `Str::snake()`
- Replaced deprecated `camel_case()` helper with `Str::camel()`
- Added PHP 7.2+ requirement
- Package now fully compatible with Laravel 6.0, 7.0, 8.0, 9.0, and 10.0

### Notes
This version maintains backward compatibility with Laravel 5.0 code patterns while adding support for Laravel 6+. All features from the original package remain functional.

---

For older releases, please look at the [project's release][1] page :)

[1]:https://github.com/laravelbook/ardent/releases
