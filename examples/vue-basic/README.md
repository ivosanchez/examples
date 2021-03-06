# vue-basic

> Project bootstrapped with [@vue/cli](https://cli.vuejs.org/)

This aims to be an example of how you would connect Flamelink with your Vue application.

View the app running [here](https://handy-potato.surge.sh)

## Setup

### Firebase Project Config

If you want to follow along:

- Ensure that you have an existing [Firebase project](https://console.firebase.google.com/u/0/) that you can use.
- Copy the `.env` file and save as `.env.local`.
- Replace all the environment variables with your Firebase project config details, for example:

Change:

```sh
VUE_APP_FLAMELINK_API_KEY="<firebase-api-key>"
```

with:

```sh
VUE_APP_FLAMELINK_API_KEY=AIzaSyDuTZiS23eqbkLA557_rlO9F0NBRZWViRx
```

#### Database Rules

To quickly make the content and navigation items available from our app without a user being authenticated, I've updated the default Flamelink Database rules to the following:

```json
{
  "rules": {
    "flamelink": {
      ".read": "auth != null",
      ".write": "auth != null",
      "environments": {
        "$env": {
          ".read": true
        }
      },
      "users": {
        ".indexOn": ["email"]
      }
    }
  }
}
```

This simply makes everything inside the `flamelink/environments` reference readable to anyone.

> **Important**! As always, once you are ready to you roll your app out to your end users, make sure to set the strictest rules possible for your use case. When it comes to these rules and security in general, it is a good idea to following the [Principle of Least Privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege). Check out: [Understanding Firebase Realtime Database Rules](https://firebase.google.com/docs/database/security/).

#### Database Structure

The following database structure was created from within the Flamelink CMS:

##### Navigation

![Main Navigation](public/img/main-navigation.png)

- Navigation Name: Main Navigation
- NaKey: mainNavigation
- Navigation Items:

```text
-- Home
    - Title: Home
    - URI: /
    - CSS Class: home-page
    - Component: Home
-- About
    - Title: About
    - URI: /about
    - CSS Class: about-page
    - Component: About
    -- Our Vision
        - Title: Our Vision
        - URI: our-vision
        - CSS Class: about-page
        - Component: OurVision
    -- Who we are
        - Title: Who we are
        - URI: who-we-are
        - CSS Class: about-page
        - Component: People
-- Contact Us
   - Title: Contact Us
   - URI: /contact-us
   - CSS Class: contact-us-page
   - Component: ContactForm
```

##### Schemas

```text
-- Home
    - Title: Home
    - Schema ID: home
    - Type: Single
    - Group: Pages
    - Enabled: true
    -- Fields:
      -- Text
          - Field Name: Page Title
          - Field Key: pageTitle
          - Show in overview table: true
      -- Textarea
          - Field Name: Page Body
          - Field Key: pageBody
          - Show in overview table: false

-- Our Vision
    - Title: Our Vision
    - Schema ID: ourVision
    - Type: Single
    - Group: Pages
    - Enabled: true
    -- Fields:
      -- Text
          - Field Name: Title
          - Field Key: title
          - Show in overview table: true
      -- Textarea
          - Field Name: Body
          - Field Key: body
          - Show in overview table: false

-- Who We Are
    - Title: Who We Are
    - Schema ID: whoWeAre
    - Type: Single
    - Group: Pages
    - Enabled: true
    -- Fields:
      -- Text
          - Field Name: Title
          - Field Key: title
          - Show in overview table: true
      -- Textarea
          - Field Name: Body
          - Field Key: body
          - Show in overview table: false
      -- Repeater
          - Field Name: People
          - Field Key: people
          - Field Layout: Table
          - Show in overview table: false
          -- Fields:
            -- Text
              - Field Name: Name
              - Field Key: name
            -- Text
              - Field Name: Job Title
              - Field Key: jobTitle
            -- Textarea
              - Field Name: Bio
              - Field Key: bio
            -- Media
              - Field Name: Avatar
              - Field Key: avatar
              - Selection Limit: 1
              - Media Types: Images
```

##### Content

Make sure you add any data for the fields we've created in our schema

### Install dependencies

```bash
yarn install
```

### Compiles and hot-reloads for development

```bash
yarn run serve
```

### Compiles and minifies for production

```bash
yarn run build
```

### Lints and fixes files

```bash
yarn run lint
```
