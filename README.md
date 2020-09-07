# oauth2-discord

![Build Status](https://gitlab.com/SiegeGG/discord-oauth2/badges/master/pipeline.svg)

Enables PHP-based websites (such as Laravel ones) to use Discord as login and/or register system.

This repo is a **fork of [team-reflex/oauth2-discord](https://github.com/teamreflex/oauth2-discord)**. Team Reflex' package was last updated on Oct 7, 2016 and we at SiegeGG need an updated version. We'll possibly add more non-breaking features but will try to leave the package fully backwards compatible.

Provides Discord OAuth 2.0 support for PHP League's [OAuth 2.0 Client](https://github.com/thephpleague/oauth2-client).

## Installation

Run `composer require kevslashnull/oauth2-discord`.

## Usage

```php
<?php

$provider = new \Discord\OAuth\Discord([
	'clientId'     => 'oauth-app-id',
	'clientSecret' => 'oauth-app-secret',
	'redirectUri'  => 'http://your.redirect.url',
]);

if (!isset($_GET['code'])) {
	echo '<a href="'.$provider->getAuthorizationUrl().'">Login with Discord</a>';
} else {
	$token = $provider->getAccessToken('authorization_code', [
		'code' => $_GET['code'],
	]);

	// Get the user object.
	$user = $provider->getResourceOwner($token);

	// Get the guilds and connections.
	$guilds = $user->guilds;
	$connections = $user->connections;

	// Accept an invite
	$invite = $user->acceptInvite('https://discord.gg/52a9dsR');

	// Get a refresh token
	$refresh = $provider->getAccessToken('refresh_token', [
		'refresh_token' => $getOldTokenFromMemory->getRefreshToken(),
	]);

	// Store the new token.
}
```

## Credits

- @KevSlashNull at [SiegeGG](https://gitlab.com/SiegeGG)
- [David Cole](https://github.com/uniquoooo)
- [All Contributors](https://github.com/teamreflex/oauth2-discord/contributors)

## License

This code is subject to the MIT license which can be found in the [LICENSE](LICENSE) file.
