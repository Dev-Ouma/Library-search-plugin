# Library Search Block for Moodle

![Moodle 4.1+](https://img.shields.io/badge/Moodle-4.1%2B-F98012?logo=moodle&logoColor=white)
![License: GPL v3](https://img.shields.io/badge/license-GPL%20v3-blue)
![Release 1.0.0](https://img.shields.io/badge/release-1.0.0-green)

A Moodle dashboard block that puts your institution's library search inside the LMS. Students search books, journals and theses without leaving Moodle, and results open in your library system (EBSCO, Koha, DSpace or any search URL).

## Features

- **Integrated search** from any Moodle page or dashboard.
- **Configurable library URL and search path**, so it works with any catalogue that accepts a query string.
- **Optional single sign-on** to the library: HMAC-signed token or email passthrough.
- **Quick links** to e-books, journals, repository and OPAC, which admins can switch on or off.
- **Customisable** block title and placeholder text.
- **Responsive**, using Moodle's Boost theme and AMD modules.
- **Privacy API** provider included.

## Requirements

- Moodle 4.1 or later
- A library system with a search URL that accepts a query parameter

## Installation

```bash
cd /path/to/moodle/blocks
git clone https://github.com/Dev-Ouma/OUK-Library-search-plugin.git librarysearch
chown -R www-data:www-data librarysearch
```

Then log in as an administrator and open **Site administration > Notifications** to finish the install. See [INSTALL.md](INSTALL.md) for the manual-upload route, upgrades and troubleshooting.

The folder name must be exactly `librarysearch`.

## Configuration

Go to **Site administration > Plugins > Blocks > Library Search**.

| Setting | Purpose |
|---|---|
| Library base URL | Main URL of your library search page |
| Search path | Query string appended to the base URL, for example `?q=` |
| Open in new tab | Open results in a new browser tab |
| Quick links | Show or hide the quick-link buttons |
| Block title / placeholder | Customise visible text |
| SSO | Enable single sign-on and choose the method |

## Single sign-on

SSO is optional and off by default. Methods in the settings page:

- **HMAC token**: sends a base64 string containing `email|timestamp|hash`. The hash uses a shared secret. Recommended for Koha, DSpace and other custom systems.
- **Email**: sends the user's email address. Use only in trusted, internal setups.

The settings page also lists JWT, OAuth 2 and CAS entries. Treat those as work in progress and test them in your own environment before relying on them.

Always use a long random shared secret (32 characters or more) and keep it only in the plugin settings, never in code.

## Development

- Component: `block_librarysearch`
- Stack: PHP, Moodle AMD (`amd/src/search.js`), Mustache templates
- Rebuild the minified JavaScript with Moodle's Grunt: `npx grunt amd`

Issues and pull requests are welcome.

## License

Released under the [GNU GPL v3 or later](LICENSE), the same licence as Moodle.
