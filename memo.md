##　セットアップ
### canvas要素を用意する
Three.jsはHTML5のcanvas要素を利用するため、canvasタグを設置し`id`を設定しておく。
```
<body>
  <canvas id="myCanvas"></canvas>
</body>
```

### Three.jsライブラリを読み込んでおく
```
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/105/three.min.js"></script>
```

WebGLの処理はページの読み込みが終わってから実行させます。`addEventListener()`関数を使ってloadイベントが発生するのを監視させ、ページが読み込み終わったときに実行させたい関数を指定します。この関数init()の中にThree.jsのコードを書いていきます。
<script>
window.addEventListener('load', init);
function init(){
  // 処理
}
</script>


### THREE.WebGLRendererでレンダラーを作成
```
const renderer = new THREE.WebGLREnderer({
  canvas: docuemnt.querySelector('#myCanvas);
});
```

### setSize()メソッドでレンダラーのサイズを設定する
第一引数がwidth。第二引数がheight。
```
const width = 960;
const height = 540;
renderer.setSize(width, height);
```

### new THREE.Scene()クラスでシーンを作成する
シーンとは3D空間のことで、3Dオブジェクトや光源などの置き場となる。
```
const scene = new.THREE.Scene();
```

### new THREE.PerspectiveCamera()クラスでカメラを作る
3Dではどの視点で空間を撮影するかと言う実装をする。
この機能は「視点」や「カメラ」と呼ばれる。

Three.jsではTHREE.PerspectiveCameraクラスのコンストラクターで画角、アスペクト比、描画開始距離、描画終了距離の4つの情報を引数として渡しカメラを作成します。
```
const width = 960;
const height = 540;
const angle = 45;
// 引数：画角、幅、高さ
const camera = new.THREEPerspectiveCamera(angle, width, height)
```

### 立方体を作る
立方体はメッシュという表示オブジェクトを使用して作成する。
メッシュを作るには、ジオメトリ（形状）とマテリアル（素材）の二種類を用意する必要がある。
ジオメトリとは頂点情報や面情報を持っている。
Three.jsには様々なジオメトリが用意されているが、今回は立方体や直方体のような形状を生成するための`BoxGeometry`を使用する。
```
// new THREE.BoxGeometry(幅、高さ、奥行き)
const geometry = new THREE.BoxGeomotry(500, 500, 500)
```

マテリアルは色や質感の情報を持っています。
今回はとりあえず箱を表示させたいので、`THREE.MeshNormalMaterial`と言う適当なカラーを割り当てるマテリアルを生成します。
```
const material = new THREE.MeshNormalMaterial();
```

作成したジオメトリとマテリアルを使って、メッシュを作ります。
作成したメッシュをシーンに追加しましょう。
```
// new THREE.Mesh(ジオメトリ, マテリアル)
const box = new THREE.Mesh(geometry, material)
// シーンに追加
scene.add(box)
```