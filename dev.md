# Code Documentation for Element 5

Includes:
* Arc Rotate Camera
* Mesh cloning
* Physics objects
* GUI with scene transitions and Buttons
* Movable object with keyboard input
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
# MenuScene.ts
# Creates the main menu scene

# createSceneButton
# Purpose: Creates GUI button to allow the user to access two other scenes (This is used elsewhere for other purposes, however since they are almost identical, I won't mention them individually)
```typescript
function createSceneButton(scene: Scene, name: string, index: string, x: string, y: string, advtex, sceneName: int,){
   var button = GUI.Button.CreateSimpleButton(name, index);
   button.left = x;
   button.top = y;
   button.width = "160px"
   button.height = "60px";
   button.color = "white";
   button.cornerRadius = 20;
   button.background = "green";
   const buttonClick = new Sound("MenuClickSFX", "./audio/menu-click.wav", scene, null, {
    loop: false,
    autoplay: false,
   });
   button.onPointerUpObservable.add(function() {
   buttonClick.play();
   setSceneIndex(sceneName);
   });
   advtex.addControl(button);
   return button;
  } 
```
# Options.ts
# Re-used file from Element 4. Uses exclusively buttons, which have already been mentioned. All of the buttons play sounds from the cartoon show "Ed, Edd 'n' Eddy"

# GameScene.ts
# A small Physics playground used to play around with the havok physics engine

# ScreenText
# Purpose: Creates GUI text to tell the player how they can spin the "blade"
```TypeScript
async function ScreenText(scene: Scene, textName: string, words: string, advtex) // I have no idea what an async function is but the code doesn't work without it so I'm keeping it until it breaks something
{
  var text = new GUI.TextBlock(textName, words);
  text.left = "0px";
  text.top = "240px";
  text.width = "240px";
  text.height = "60px";
  text.color = "white";
  text.fontSize = 16;
  advtex.addControl(text);

  return text;
}
```
# CreateBox, CloneBox, CreateSphere, CloneSphere
# Purpose: Creates example objects to be cloned into objects with physics properties
```TypeScript
//droppables and Ground
function CreateBox(scene, x, y, z){
  let box: Mesh = MeshBuilder.CreateBox("box", scene);
  box.position.x = x;
  box.position.y = y;
  box.position.z = z;
  
  return box;
 }
//Clone box
function CloneBox(scene: Scene, Cloned: Mesh){
  const clone = Cloned.clone("Box clone");
  const boxAggregate = new PhysicsAggregate(clone, PhysicsShapeType.BOX, { mass: 10 }, scene);
  return clone;
}
function CreateSphere(scene, x, y, z){
  let sphere: Mesh = MeshBuilder.CreateSphere("sphere", scene);
  sphere.position.x = x;
  sphere.position.y = y;
  sphere.position.z = z;
  
  return sphere;
 }
//Clone Sphere
function CloneSphere(scene: Scene, Cloned: Mesh){
  const clone = Cloned.clone("Sphere clone");
  const boxAggregate = new PhysicsAggregate(clone, PhysicsShapeType.SPHERE, { mass: 10 }, scene);
  return clone;
}
 //----
 function CreateGround(scene: Scene) {
  const ground: Mesh = MeshBuilder.CreateGround("ground", {height: 40, width: 40, subdivisions: 4});
  const groundAggregate = new PhysicsAggregate(ground, PhysicsShapeType.BOX, { mass: 0 }, scene);
  return ground;
 }
```
# End of Code Documentation

