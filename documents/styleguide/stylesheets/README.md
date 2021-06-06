# 🎨 Stylesheets

## SCSS
- Although the application can handle `.css`, write all new stylesheets in `.scss`

## Custom Variables
- Union variables can be imported with the `@value` keyword
- Union variables should be used over hard coding the value
```scss
@value varSpBase from '@xo-union/tk-css-spacing';
@value varCoolgray100 from '@xo-union/tk-ui-colors';

// Good
.content {
  background-color: varCoolgray100;
  margin-top: varSpBase;
}

// Bad
.data {
  background-color: #999;
  margin-top: 6px;
}
```