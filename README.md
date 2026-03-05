# Earth Globe With Three.js

## Overview:
This is an innovative web application presenting a captivating 3D model of the Earth using Three.js and WebGL technologies. Users can navigate and interact with a realistic globe, featuring dynamic lighting, shadows, and responsive controls.

## Key Features:
- **3D Earth Model**: The application showcases a high-fidelity 3D model of the Earth, allowing users to explore and examine geographical details with immersive graphics.

- **Interactive Controls**: Users can rotate and play with the 3D Earth model using responsive controls, providing an intuitive and engaging experience.

- **WebGL and Three.js**: The project leverages the power of WebGL and the Three.js library to create realistic 3D graphics directly in the web browser.

## Technologies Used:
- **Frontend: HTML, CSS, JavaScript**

- **3D Graphics: Three.js, WebGL**

- **Deployment: Vercel**

## Purpose:
This serves as a demonstration of the capabilities of WebGL and three.js in creating interactive 3D graphics on the web. It caters to individuals interested in the fusion of web development and advanced visualizations, offering a unique exploration of our planet in a virtual space
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>TRON Earth</title>
<style>
body{
  margin:0;
  overflow:hidden;
  background:black;
  color:cyan;
  font-family:monospace;
}
#hud{
  position:absolute;
  top:20px;
  left:20px;
  z-index:10;
}
button{
  background:black;
  color:cyan;
  border:1px solid cyan;
  padding:8px 12px;
}
</style>
</head>

<body>

<div id="hud">
<h2>TRON EARTH CONTROL</h2>
<button onclick="toggle()">Toggle Grid</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.min.js"></script>

<script>

const scene = new THREE.Scene();

const camera = new THREE.PerspectiveCamera(
75,
window.innerWidth/window.innerHeight,
0.1,
1000
);

const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth,window.innerHeight);
document.body.appendChild(renderer.domElement);

camera.position.z = 3;

// Earth sphere
const geometry = new THREE.SphereGeometry(1,64,64);

const material = new THREE.MeshBasicMaterial({
  color:0x00ffff,
  wireframe:true
});

const earth = new THREE.Mesh(geometry,material);
scene.add(earth);

// satellites
const satellites=[];

for(let i=0;i<20;i++){

const g=new THREE.SphereGeometry(0.02,8,8);

const m=new THREE.MeshBasicMaterial({color:0xff6600});

const sat=new THREE.Mesh(g,m);

sat.userData.angle=Math.random()*Math.PI*2;
sat.userData.radius=1.5+Math.random();

scene.add(sat);
satellites.push(sat);

}

// animation
function animate(){

requestAnimationFrame(animate);

earth.rotation.y+=0.002;

satellites.forEach(s=>{

s.userData.angle+=0.01;

s.position.x=Math.cos(s.userData.angle)*s.userData.radius;
s.position.z=Math.sin(s.userData.angle)*s.userData.radius;

});

renderer.render(scene,camera);

}

animate();

function toggle(){
earth.material.wireframe=!earth.material.wireframe;
}

</script>

</body>
</html>
