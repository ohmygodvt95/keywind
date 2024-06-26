# :wind_face: Keywind

Keywind is a component-based Keycloak Login Theme built with [Tailwind CSS](https://github.com/tailwindlabs/tailwindcss) and [Alpine.js](https://github.com/alpinejs/alpine).

![Preview](./preview.png)

### Styled Pages

- Error
- Login
- Login Config TOTP
- Login IDP Link Confirm
- Login OAuth Grant
- Login OTP
- Login Page Expired
- Login Password
- Login Recovery Authn Code Config
- Login Recovery Authn Code Input
- Login Reset Password
- Login Update Password
- Login Update Profile
- Login Username
- Login X.509 Info
- Logout Confirm
- Register
- Select Authenticator
- Terms and Conditions
- WebAuthn Authenticate
- WebAuthn Error
- WebAuthn Register

### Identity Provider Icons

- Apple
- Bitbucket
- Discord
- Facebook
- GitHub
- GitLab
- Google
- Instagram
- LinkedIn
- Microsoft
- OpenID
- Red Hat OpenShift
- PayPal
- Slack
- Stack Overflow
- Twitter

## Installation

Keywind has been designed with component-based architecture from the start, and **you can customize as little or as much Keywind as you need**:

1. [Deploy Keywind Login Theme](https://www.keycloak.org/docs/latest/server_development/#deploying-themes)
2. [Create your own Login Theme](https://www.keycloak.org/docs/latest/server_development/#creating-a-theme)
3. Specify parent theme in [theme properties](https://www.keycloak.org/docs/latest/server_development/#theme-properties):

```
parent=keywind
```

4. Brand and customize components with [FreeMarker](https://freemarker.apache.org/docs/dgui_quickstart_template.html)

## Customization

### Local development

Use docker-compose to initialize Keycloak locally, making it easy to check the results when you edit Keywind.

```bash
docker compose up -d // start keycloak for testing
```

Then, select the login theme for the client in Keycloak as Keywind.

Finally, let Vite do its job.

```bash
pnpm run dev // watch *.ftl changes and regenerate css
```

You can go to the client's login page to see. The key point here is that for realms with the display name `Keycloak` (by default),
CSS and JS will use the Vite link, while for other cases, they will still use the built link.
In `document.ftl`, this trick to enable hot reload when developing the theme and it work.

```
  <#if realm.displayName == 'Keycloak'>
    <link href="http://localhost:5173/src/index.css" rel="stylesheet">
    <script defer src="http://localhost:5173/src/index.ts" type="module"></script>
  </#if>
```

### Theme

When you do need to customize a palette, you can configure your colors under the `colors` key in the `theme` section of Tailwind config file:

`tailwind.config.js`

```js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: colors.red,
      },
    },
  },
};
```

Read more about Tailwind CSS configuration in the [documentation](https://tailwindcss.com/docs/configuration).

### Components

You can update Keywind components in your own child theme. For example, create a copy of the `body` component and change the background:

`theme/mytheme/login/components/atoms/body.ftl`

```
<#macro kw>
  <body class="bg-primary-100">
    <#nested>
  </body>
</#macro>
```

## Build

When you're ready to deploy your own theme, run the build command to generate a static production build.

```bash
pnpm install
pnpm build
```

To deploy a theme as an archive, create a JAR archive with the theme resources.

```bash
pnpm build:jar
```
