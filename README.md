# 🕹 pixi-virtual-joystick (Vanilla JS version)

Virtual Touch Joystick for [pixi.js](https://github.com/pixijs/pixi.js)

<img src="screenshot.gif?raw=1" />

## Demo

http://unitedcommand.com/apps/vjs/

## Usage

```javascript
PIXI.Loader.shared
  .add('outer', "./images/joystick.png") 
  .add('inner', "./images/joystick-handle.png")
  .load(initialize);

function initialize() {
  const app = new PIXI.Application({
    view: document.getElementById('canvas'),
    backgroundColor: 0xffffff,
    autoDensity: true,
    resolution: window.devicePixelRatio,
  });

  const leftText = new PIXI.Text("[left data]");
  const rightText = new PIXI.Text("[right data]");
  const leftJoystick = new Joystick({
    outer: PIXI.Sprite.from('outer'),
    inner: PIXI.Sprite.from('inner'),
    outerScale: { x: 0.5, y: 0.5 },
    innerScale: { x: 0.8, y: 0.8 },
    onChange: (data) => { leftText.text = JSON.stringify(data); },
    onStart: () => console.log('start'),
    onEnd: () => console.log('end'),
  });
  app.stage.addChild(leftJoystick);

  const rightJoystick = new Joystick({
    onChange: (data) => { rightText.text = JSON.stringify(data); },
    onStart: () => console.log('start'),
    onEnd: () => console.log('end'),
  });
  app.stage.addChild(rightJoystick);

  leftText.position.set(0, 0);
  rightText.position.set(0, 50);
  app.stage.addChild(leftText);
  app.stage.addChild(rightText);

  const resize = () => {
    leftJoystick.position.set(leftJoystick.width, window.innerHeight - leftJoystick.height);
    rightJoystick.position.set(window.innerWidth - rightJoystick.width, window.innerHeight - rightJoystick.height);
    app.renderer.resize(window.innerWidth, window.innerHeight);
    app.resize();
  }
  resize();
  window.addEventListener('resize', resize);

  app.start();
  
}
```

## Similar alternatives

- [nipplejs](https://github.com/yoannmoinet/nipplejs/) (more features, DOM-based)
- [react-nipple](https://github.com/loopmode/react-nipple)

## License

Endel Dreyer © MIT
