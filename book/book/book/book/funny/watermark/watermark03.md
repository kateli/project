#  2.3 自定义背景添加自定义水印

<style>
    .customizeWatermark {
      margin: 0 auto;
      text-align: center;
      padding-top: 20%;
    }

    #uploadFile {
      display: none;
    }

    .ui-button {
      color: #fff;
      border: 1px solid #00a5e0;
      background: #00a5e0;
      font-size: 14px;
      padding: 9px 15px;
      border-radius: 4px;
      cursor: pointer;
      outline: none;
    }

    .ui-button:hover {
      border: 1px solid #00b4f5;
      background-color: #00b4f5;
    }

    .text {
      width: 200px;
      padding: 12px 10px;
      border: 1px solid #ccc;
      border-radius: 3px;
      outline: none;
    }

    #imgUploaded {
      padding-top: 20px;
    }

    #imgUploaded img { 
      width: 380px;
    }
  </style>

  <div class="customizeWatermark">
    <input type="file" id="uploadFile" class="clip" accept="image/*">
    <label class="ui-button" for="uploadFile">选择图片</label>
    <input type="text" class="text" id="text" maxlength="12" />
    <button class="ui-button" id="sure">确定</button>
    <div id="imgUploaded"></div>
  </div>

  <script type="text/javascript">
    var imgUploaded = document.querySelector('#imgUploaded');
    var oSure = document.querySelector('#sure');
    var oUploadSrc = '',
      size = 180;

    function readFile(file) {
      var reader = new FileReader();
      reader.readAsDataURL(file)
      reader.onload = function (e) {
        imgUploaded.innerHTML = `<img src="${reader.result}"  />`;
        oUploadSrc = reader.result;
      }
    }
    var oFile = document.getElementById('uploadFile');
    oFile.onchange = function (e) {
      var file = e.target.files[0];
      readFile(file)
    }

    oSure.onclick = function () {
      var val = document.querySelector('#text').value;
      var oUploadedImg = imgUploaded.querySelector('img');
      if (oUploadSrc.length === 0) {
        alert("请先选择图片");
        return false;
      } else if (val.trim().length === 0) {
        alert('请输入图片的水印文字');
        return false;
      }
      var cans = document.createElement('canvas');
      var canW = oUploadedImg.width;
      var canH = oUploadedImg.height;
      cans.width = canW;
      cans.height = canH;
      var ctx = cans.getContext('2d');
      var grd = ctx.createLinearGradient(0, 0, canW, 0)
      var img = new Image();
      img.src = oUploadSrc;
      img.onload = function () {
        ctx.drawImage(img, 0, 0, canW, canH);
        ctx.font = "30px 华文隶书";
        grd.addColorStop(0, 'red')
        grd.addColorStop(0.2, 'orange')
        grd.addColorStop(0.4, 'yellow')
        grd.addColorStop(0.6, 'green')
        grd.addColorStop(0.8, 'blue')
        grd.addColorStop(1, 'indigo')
        ctx.fillStyle = grd;
        const textW = Math.round(ctx.measureText(`@${val}`).width);
        const x = canW - textW <= 0 ? 0 : canW - textW;
        ctx.fillText(`@${val}`, x, canH - 20);
        var url = cans.toDataURL();
        imgUploaded.innerHTML = `<img src="${url}" />`;
      }

    }
  </script>
  