# Fake GlassBrowser based on Vue.js+Vuetify 3
Since we were bored to present our screenshots in billions of different ways, here at [umbertogiacobbi.biz](https://umbertogiacobbi.biz) we decided (we need to show some screens for our [aginti.it](https://aginti.it) project) to create our own "fake" next-gen super cool glassmoriphism browser.

This is a typical example of how a startup can same some bucks implementing a software, a custom photo shootin setup in a corner, use open source software and more to overcome the scarsicity of resources. We're all on the same boat guys!

This is a simple **vVue3 + Vuetify3** node.js project so is meant to run locally.

Download it, the background images changes randomly at each load (see them in the backgrounds folder) so each time you have a different background.

To change the "browser content just change the **yourScreenshot.jpg** file you'll find in the images folder.

The aim is not only make it static but also dynamic in case you need to record a short video for a demo.

Some random ideas that someone could come up and fix:

 - Support dark/light theme, there is a button in the toolbar but does nothing
 - Add the possibility to add an iframe or whatever and see your live site for demo?
 - Navigation anyone? I will add back/next button I think, but their functionality is linked to the one above.
 - If I had any other idea I will write here...

I keep it as basic as possible using only CSS.

Feel free to reuse it, improve it or whatever.

Regards, Umberto Giacobbi
UmbertoGiacobbiDotBiz Founder

hello@umbertogiacobbi.biz

## And this is the result as of today with the admin panel
![image](https://github.com/umbertotechnopreneur/glassBrowser/assets/12001165/7fc8ad34-37c5-4794-8df2-863ec2aaf6b4)
## And this without
![image](https://github.com/umbertotechnopreneur/glassBrowser/assets/12001165/36cf1073-dc7f-41ab-a078-712481117aca)

## Project setup

```
# yarn
yarn

# npm
npm install

# pnpm
pnpm install

# bun
bun install
```

### Compiles and hot-reloads for development

```
# yarn
yarn dev

# npm
npm run dev

# pnpm
pnpm dev

# bun
bun run dev
```

### Compiles and minifies for production

```
# yarn
yarn build

# npm
npm run build

# pnpm
pnpm build

# bun
bun run build
```

### Customize configuration

See [Configuration Reference](https://vitejs.dev/config/).
