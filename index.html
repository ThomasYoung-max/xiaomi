<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>黎曼曲面 · w = √z</title>
<style>
  :root{
    --ui-bg: rgba(14,18,32,.62);
    --ui-bd: rgba(140,190,255,.22);
    --ui-fg: #cfe4ff;
  }
  *{box-sizing:border-box}
  html,body{
    margin:0;height:100%;overflow:hidden;background:#04060c;
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI","PingFang SC","Microsoft YaHei",sans-serif;
  }
  #app{position:fixed;inset:0}
  canvas{display:block}

  .hud{
    position:fixed;top:22px;left:26px;pointer-events:none;color:var(--ui-fg);
    text-shadow:0 0 20px rgba(90,160,255,.6);
  }
  .hud h1{margin:0;font-size:20px;font-weight:600;letter-spacing:.08em}
  .hud h1 b{font-weight:800;color:#8fd4ff}
  .hud p{margin:9px 0 0;font-size:12.5px;opacity:.58;letter-spacing:.06em}

  .btns{
    position:fixed;left:26px;bottom:26px;display:flex;gap:10px;flex-wrap:wrap;
    max-width:calc(100vw - 52px);
  }
  .btns button{
    appearance:none;border:1px solid var(--ui-bd);
    background:var(--ui-bg);backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);
    color:var(--ui-fg);font-size:13px;font-family:inherit;letter-spacing:.05em;
    padding:9px 17px;border-radius:999px;cursor:pointer;transition:.22s ease;
  }
  .btns button:hover{
    background:rgba(70,130,220,.3);border-color:rgba(150,205,255,.55);
    transform:translateY(-1px);box-shadow:0 6px 22px rgba(60,130,255,.25);
  }
  .btns button.off{opacity:.42}

  .legend{
    position:fixed;right:26px;bottom:26px;color:var(--ui-fg);opacity:.5;
    font-size:12px;letter-spacing:.05em;text-align:right;line-height:1.7;
    pointer-events:none;
  }
</style>
</head>
<body>
<div id="app"></div>

<div class="hud">
  <h1>黎曼曲面 &nbsp;<b>w = √z</b></h1>
  <p>拖动旋转 · 滚轮缩放 · 右键平移</p>
</div>

<div class="btns">
  <button id="btnRotate">自动旋转</button>
  <button id="btnGrid">网格线</button>
  <button id="btnReset">重置视角</button>
</div>

<div class="legend">
  两片叶面沿正实轴相接<br>原点为支点 (branch point)
</div>

<script type="importmap">
{
  "imports": {
    "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
    "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
  }
}
</script>

<script type="module">
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

/* ============================================================
   1. 渲染器 / 场景 / 相机
   ============================================================ */
const app = document.getElementById('app');

const renderer = new THREE.WebGLRenderer({ antialias: true });
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.toneMapping = THREE.ACESFilmicToneMapping;
renderer.toneMappingExposure = 1.12;
renderer.outputColorSpace = THREE.SRGBColorSpace;
app.appendChild(renderer.domElement);

const scene = new THREE.Scene();
scene.background = new THREE.Color(0x04060c);
scene.fog = new THREE.FogExp2(0x04060c, 0.026);

const camera = new THREE.PerspectiveCamera(
  46, window.innerWidth / window.innerHeight, 0.05, 200
);
camera.position.set(4.2, 3.1, 4.6);

const controls = new OrbitControls(camera, renderer.domElement);
controls.enableDamping = true;
controls.dampingFactor = 0.07;
controls.rotateSpeed = 0.85;
controls.zoomSpeed = 0.9;
controls.panSpeed = 0.8;
controls.minDistance = 1.0;
controls.maxDistance = 26;
controls.autoRotate = true;
controls.autoRotateSpeed = 0.55;
controls.target.set(0, 0, 0);

/* ============================================================
   2. 环境贴图（用 canvas 生成柔和渐变）
   ============================================================ */
(function buildEnv() {
  const cv = document.createElement('canvas');
  cv.width = 8; cv.height = 128;
  const ctx = cv.getContext('2d');
  const g = ctx.createLinearGradient(0, 0, 0, 128);
  g.addColorStop(0.00, '#3a5fa8');
  g.addColorStop(0.45, '#141d33');
  g.addColorStop(1.00, '#4a1436');
  ctx.fillStyle = g;
  ctx.fillRect(0, 0, 8, 128);
  const tex = new THREE.CanvasTexture(cv);
  tex.mapping = THREE.EquirectangularReflectionMapping;
  tex.colorSpace = THREE.SRGBColorSpace;
  scene.environment = tex;
})();

/* ============================================================
   3. 灯光
   ============================================================ */
scene.add(new THREE.HemisphereLight(0x7fa8ff, 0x2a0a33, 0.75));

const lightA = new THREE.PointLight(0x5fc8ff, 120, 60, 2);
lightA.position.set(7, 7, 6);
scene.add(lightA);

const lightB = new THREE.PointLight(0xff4fa0, 90, 60, 2);
lightB.position.set(-7, -5, -6);
scene.add(lightB);

const lightC = new THREE.DirectionalLight(0xffffff, 1.15);
lightC.position.set(3, 8, 4);
scene.add(lightC);

const lightD = new THREE.PointLight(0xffe08a, 40, 40, 2);
lightD.position.set(0, -6, 3);
scene.add(lightD);

/* ============================================================
   4. 曲面参数化
      z = r·e^{iu},  u ∈ [0, 4π)
      w = √r · e^{iu/2}
      嵌入三维： ( Re z , Im w , Im z )
   ============================================================ */
const R_MAX = 2.0;      // 最大半径
const NU    = 400;      // 角度方向采样（覆盖 4π）
const NR    = 56;       // 径向采样
const POW   = 1.35;     // 径向采样幂（原点附近更密）

function surfacePoint(rad, u, out) {
  const h = Math.sqrt(rad) * Math.sin(u * 0.5);
  out.set(rad * Math.cos(u), h, rad * Math.sin(u));
  return out;
}

const surfGeo = new THREE.BufferGeometry();
{
  const vCount = (NU + 1) * (NR + 1);
  const posArr = new Float32Array(vCount * 3);
  const colArr = new Float32Array(vCount * 3);
  const uvArr  = new Float32Array(vCount * 2);
  const idxArr = new Uint32Array(NU * NR * 6);

  const col = new THREE.Color();
  let ip = 0, ic = 0, iu = 0, ii = 0;

  for (let i = 0; i <= NU; i++) {
    const u    = (i / NU) * Math.PI * 4;   // 0 → 4π
    const half = Math.sin(u * 0.5);
    const cu   = Math.cos(u);
    const su   = Math.sin(u);
    const hu   = i / NU;                   // 0 → 1（色相绕一整圈，首尾衔接）

    for (let j = 0; j <= NR; j++) {
      const t   = j / NR;
      const rad = R_MAX * Math.pow(t, POW);
      const h   = Math.sqrt(rad) * half;

      // 位置
      posArr[ip++] = rad * cu;
      posArr[ip++] = h;
      posArr[ip++] = rad * su;

      // UV
      uvArr[iu++] = hu;
      uvArr[iu++] = t;

      // 顶点颜色：沿 u 环绕色相，中心略亮
      const sat   = 0.74;
      const light = 0.55 - 0.14 * t;
      col.setHSL(hu, sat, light);
      colArr[ic++] = col.r;
      colArr[ic++] = col.g;
      colArr[ic++] = col.b;
    }
  }

  // 索引
  const stride = NR + 1;
  for (let i = 0; i < NU; i++) {
    for (let j = 0; j < NR; j++) {
      const a =  i      * stride + j;
      const b = (i + 1) * stride + j;
      const c = (i + 1) * stride + j + 1;
      const d =  i      * stride + j + 1;
      idxArr[ii++] = a; idxArr[ii++] = b; idxArr[ii++] = d;
      idxArr[ii++] = b; idxArr[ii++] = c; idxArr[ii++] = d;
    }
  }

  surfGeo.setAttribute('position', new THREE.BufferAttribute(posArr, 3));
  surfGeo.setAttribute('color',    new THREE.BufferAttribute(colArr, 3));
  surfGeo.setAttribute('uv',       new THREE.BufferAttribute(uvArr, 2));
  surfGeo.setIndex(new THREE.BufferAttribute(idxArr, 1));
  surfGeo.computeVertexNormals();
}

/* ============================================================
   5. 曲面材质（带缓慢流动的光波）
   ============================================================ */
const surfMat = new THREE.MeshStandardMaterial({
  vertexColors: true,
  side: THREE.DoubleSide,
  metalness: 0.34,
  roughness: 0.30,
  transparent: true,
  opacity: 0.93,
  depthWrite: true,
  envMapIntensity: 0.9
});

surfMat.onBeforeCompile = (shader) => {
  shader.uniforms.uTime = { value: 0 };

  shader.vertexShader =
    'varying float vUU;\n' +
    shader.vertexShader.replace(
      '#include <begin_vertex>',
      '#include <begin_vertex>\n  vUU = uv.x;'
    );

  shader.fragmentShader =
    'varying float vUU;\nuniform float uTime;\n' +
    shader.fragmentShader.replace(
      '#include <color_fragment>',
      `#include <color_fragment>
       float wv = sin(vUU * 25.1327 - uTime * 1.35) * 0.5 + 0.5;
       diffuseColor.rgb *= (0.84 + 0.34 * wv);`
    );

  surfMat.userData.shader = shader;
};

const surface = new THREE.Mesh(surfGeo, surfMat);
surface.renderOrder = 1;
scene.add(surface);

/* ============================================================
   6. 网格线（等 r 圆环 + 等 u 辐条）
   ============================================================ */
const gridGroup = new THREE.Group();
scene.add(gridGroup);

{
  const lineMat = new THREE.LineBasicMaterial({
    color: 0xbfe4ff,
    transparent: true,
    opacity: 0.20,
    depthWrite: false
  });

  const P = new THREE.Vector3();

  // 等 r 圆环
  const RADII = [0.40, 0.70, 1.05, 1.45, 1.80, 2.00];
  const M1 = 420;
  for (const rad of RADII) {
    const pts = [];
    for (let k = 0; k <= M1; k++) {
      const u = (k / M1) * Math.PI * 4;
      surfacePoint(rad, u, P);
      pts.push(P.clone());
    }
    const g = new THREE.BufferGeometry().setFromPoints(pts);
    gridGroup.add(new THREE.Line(g, lineMat));
  }

  // 等 u 辐条
  const US = 24;
  const M2 = 70;
  for (let k = 0; k < US; k++) {
    const u = (k / US) * Math.PI * 4;
    const pts = [];
    for (let m = 0; m <= M2; m++) {
      const rad = R_MAX * Math.pow(m / M2, POW);
      surfacePoint(rad, u, P);
      pts.push(P.clone());
    }
    const g = new THREE.BufferGeometry().setFromPoints(pts);
    gridGroup.add(new THREE.Line(g, lineMat));
  }
}

/* ============================================================
   7. 支点标记（原点）
   ============================================================ */
{
  const dot = new THREE.Mesh(
    new THREE.SphereGeometry(0.045, 20, 20),
    new THREE.MeshBasicMaterial({ color: 0xffe9a8 })
  );
  scene.add(dot);

  // 柔和光晕
  const cv = document.createElement('canvas');
  cv.width = cv.height = 128;
  const ctx = cv.getContext('2d');
  const g = ctx.createRadialGradient(64, 64, 0, 64, 64, 64);
  g.addColorStop(0.0, 'rgba(255,230,150,1)');
  g.addColorStop(0.25, 'rgba(255,190,90,0.45)');
  g.addColorStop(1.0, 'rgba(255,160,60,0)');
  ctx.fillStyle = g;
  ctx.fillRect(0, 0, 128, 128);

  const glowTex = new THREE.CanvasTexture(cv);
  glowTex.colorSpace = THREE.SRGBColorSpace;
  const glow = new THREE.Sprite(new THREE.SpriteMaterial({
    map: glowTex,
    transparent: true,
    blending: THREE.AdditiveBlending,
    depthWrite: false,
    depthTest: true
  }));
  glow.scale.set(0.95, 0.95, 0.95);
  scene.add(glow);
}

/* ============================================================
   8. 交互按钮
   ============================================================ */
const btnRotate = document.getElementById('btnRotate');
const btnGrid   = document.getElementById('btnGrid');
const btnReset  = document.getElementById('btnReset');

btnRotate.addEventListener('click', () => {
  controls.autoRotate = !controls.autoRotate;
  btnRotate.classList.toggle('off', !controls.autoRotate);
});

btnGrid.addEventListener('click', () => {
  gridGroup.visible = !gridGroup.visible;
  btnGrid.classList.toggle('off', !gridGroup.visible);
});

btnReset.addEventListener('click', () => {
  controls.target.set(0, 0, 0);
  camera.position.set(4.2, 3.1, 4.6);
  controls.update();
});

/* ============================================================
   9. 动画循环
   ============================================================ */
const clock = new THREE.Clock();

function animate() {
  requestAnimationFrame(animate);

  const t  = clock.getElapsedTime();

  // 流动光波
  const sh = surfMat.userData.shader;
  if (sh) sh.uniforms.uTime.value = t;

  // 灯光缓缓环绕
  lightA.position.set(Math.cos(t * 0.34) * 8, 6.5, Math.sin(t * 0.34) * 8);
  lightB.position.set(Math.cos(t * 0.34 + Math.PI) * 8, -5.5, Math.sin(t * 0.34 + Math.PI) * 8);
  lightD.position.set(Math.cos(t * 0.5 + 1.2) * 4, -6, Math.sin(t * 0.5 + 1.2) * 4);

  controls.update();
  renderer.render(scene, camera);
}
animate();

/* ============================================================
   10. 自适应窗口
   ============================================================ */
window.addEventListener('resize', () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
});
</script>
</body>
</html>
