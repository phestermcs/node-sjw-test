### Fixes - "mainx" - `sym-x-file -> ../index.js`

#### Spec
```javascript
const $mainx = process.platform === 'win32' ? '$main.jx' : '$main.jx:777'

test('fix-main-x-file-sl-rel-target', t => {
  testfix(t, 'node_modules/bin/main.jx', {
    realdir: {
      node_modules: {
        anc: mod('anc_1'),
        main: mod('main_1', ['anc', 'desc'], {
          node_modules: {
            desc: mod('desc_1')
          }
        }),
      },
    },
    node_modules: {
      anc: mod('anc_WRONG'),
      bin: {
        [$mainx]: '../../realdir/node_modules/main/index.js',
        node_modules: {
          desc: mod('desc_WRONG')
        }
      }
    },
  })
})
```

#### `sjw.on`
```
node   : v7.2.0-sjw  NODE_SUPPORT_SYMLINKS = 1
date   : Sat, 03 Dec 2016 17:27:21 GMT
'$'    : 'C:\src\node-sjw-test\test\_layouts'
'_'    : '$\fix-main-x-file-sl-rel-target'

require              linked    ld/ksh  __dirname                  realpath
-------------------  --------  ------  -------------------------  -- key -
node '_\index.js'    [main_1]  LOADED  _\realdir\nm\main          <-
 [main_1] <anc>      [anc_1]   LOADED  _\realdir\nm\anc           <-
 [main_1] <desc>     [desc_1]  LOADED  _\realdir\nm\main\nm\desc  <-

caller               called    ()-cnt  __dirname                  realpath
-------------------  --------  ------  -------------------------  -- key -
node '_\index.js'()  [main_1]     1    _\realdir\nm\main          <-
  [main_1] <anc>()   [anc_1]      1    _\realdir\nm\anc           <-
  [main_1] <desc>()  [desc_1]     1    _\realdir\nm\main\nm\desc  <-
```

#### `rel.on`
```
node   : v7.2.0  NODE_PRESERVE_SYMLINKS = 1
date   : Sat, 03 Dec 2016 17:27:22 GMT
'$'    : 'C:\src\node-sjw-test\test\_layouts'
'_'    : '$\fix-main-x-file-sl-rel-target'

require              linked    ld/ksh  __dirname                  realpath
-------------------  --------  ------  ------------------- key -  --------
node '_\index.js'    [main_1]  LOADED  _\realdir\nm\main          <-
 [main_1] <anc>      [anc_1]   LOADED  _\realdir\nm\anc           <-
 [main_1] <desc>     [desc_1]  LOADED  _\realdir\nm\main\nm\desc  <-

caller               called    ()-cnt  __dirname                  realpath
-------------------  --------  ------  ------------------- key -  --------
node '_\index.js'()  [main_1]     1    _\realdir\nm\main          <-
  [main_1] <anc>()   [anc_1]      1    _\realdir\nm\anc           <-
  [main_1] <desc>()  [desc_1]     1    _\realdir\nm\main\nm\desc  <-
```

