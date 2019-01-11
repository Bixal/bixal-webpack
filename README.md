# Set up your decoupled environment:

1. Create apps using create-react-app or place in /apps.

   _note:_ If you're using `npx create-react-app your-react-app` you'll need to
   delete the `node_modules` folder to avoid errors on `npm run-script build`.

2) Merge the package.json files to ./package.json and delete them from the individual apps.

3) Run: 'npm install'

4) Create a block for your app in: web/modules/custom/YOURMODULE/src/Plugin/Block/.

5) Run: 'npm run build'

6) Add app to YOURMODULE.libraries.yml.

```yml
your-app:
  version: 1.x
  css:
    theme:
      tools/build/static/css/your-app.min.css: {}
  js:
    tools/build/static/js/your-app.min.js: {}
```

7. Create a Block for your app.

```php
?php

namespace Drupal\YOURMODULE\Plugin\Block;

use Drupal\Core\Block\BlockBase;

/**
 * Provides a 'YourAppBlock' block.
 *
 * @Block(
 *  id = "your_app_block",
 *  admin_label = @Translation("Your app block"),
 * )
 */
class YourAppBlock extends BlockBase {

  /**
   * {@inheritdoc}
   */
  public function build() {
    $build = [];
    $build['your_app_block']['#attached']['library'][] = 'YOURMODULE/your-app';
    $build['your_app_block']['#markup'] = '<div id="your-app"></div>';
    $build['#cache'] = ['max-age' => 0];

    return $build;
  }

}
```

8. Make sure the div id matches the id defined in your-app/src/index.js

```javascript
ReactDOM.render(<App />, document.getElementById("your-app"));
```
