<link rel="stylesheet" href="../../assets/button.css" type="text/css">
# 2.4 拼图游戏

<style>
    * {
      margin: 0;
      padding: 0;
    }

    .puzzle {
      width: 300px;
      height: 300px;
      display: flex;
      flex-wrap: wrap;
      margin: 0 auto;
    }

    .puzzle div {
      width: 100px;
      text-align: center;
      line-height: 100px;
      font-size: 30px;
	  color:#ddd;
    }

    .puzzle div:nth-child(1) {
      background: red
    }

    .puzzle div:nth-child(2) {
      background: orange
    }

    .puzzle div:nth-child(3) {
      background: purple
    }

    .puzzle div:nth-child(4) {
      background: green
    }

    .puzzle div:nth-child(5) {
      background: Magenta
    }

    .puzzle div:nth-child(6) {
      background: yellow
    }

    .puzzle div:nth-child(7) {
      background: Indigo
    }

    .puzzle div:nth-child(8) {
      background: pink
    }

    .puzzle div:nth-child(9) {
      background: blue
    }

    .step {
      text-align: center;
      padding: 30px 0 60px;
    }

    .btns {
      width: 200px;
      height: 100px;
      position: relative;
      margin: 0 auto;
    }

    .btns button {
      position: absolute;
      margin: 0;
    }

    .btns button:nth-child(1) {
      top: 0;
      left: 50%;
      transform: translateX(-50%);
    }

    .btns button:nth-child(2) {
      bottom: 0;
      left: 50%;
      top: auto;
      transform: translateX(-50%);
    }

    .btns button:nth-child(3) {
      top: 50%;
      left: 0;
      transform: translateY(-50%);
    }

    .btns button:nth-child(4) {
      top: 50%;
      right: 0;
      transform: translateY(-50%);
    }

    .reset {
      text-align: center;
      padding-top: 30px;
    }
  </style>

  <div class="puzzle">
  </div>
  <div class="reset">
    <button id="reset">重置</button>
  </div>
  <div class="step">
    当前步数：<span id="num">0</span>步
  </div>
  <div class="btns">
    <button data-type="1">↑</button>
    <button data-type="2">↓</button>
    <button data-type="3">←</button>
    <button data-type="4">→</button>
  </div>


  <script type="text/javascript">
    var arr = [0, 1, 2, 3, 4, 5, 6, 7, 8];
    var oPuzzle = document.querySelector('.puzzle');
    var oBtns = document.querySelector('.btns');
    var oReset = document.querySelector('#reset');
    var oNum = document.querySelector('#num');
    var currentArr = arr.sort(() => Math.random() - 0.5);
    var num = 0;

    render(currentArr)
    //创建九宫格
    function render(currentArr) {
      oPuzzle.innerHTML = "";
      currentArr.forEach(item => {
        var oDiv = document.createElement('div');
        item = item ? item : ""
        oDiv.innerHTML = item
        oPuzzle.appendChild(oDiv)
      })
      if (currentArr.join('') === '123456780') {
        alert("好厉害，拼成功了")
      }
    }

    //重置：
    oReset.onclick = function () {
      currentArr = arr.sort(() => Math.random() - 0.5);
      render(currentArr)
    }

    // 控制键
    oBtns.addEventListener('click', (e) => {
      var type = e.target.getAttribute('data-type');
      var zero = currentArr.indexOf(0);
      var target;
      if (type) {
        if (type === "1") {
          if (zero > 5) {
            return false
          }
          target = zero + 3
        }
        if (type === "2") {
          if (zero < 3) {
            return false;
          }
          target = zero - 3
        }
        if (type === "3") {
          if ([2, 5, 8].includes(zero)) {
            return false
          }
          target = zero + 1
        }
        if (type === "4") {
          if ([0, 3, 6].includes(zero)) {
            return false
          }
          target = zero - 1
        }
        num++;
        oNum.innerHTML = num;
        var temp = currentArr[target]
        currentArr[target] = 0;
        currentArr[zero] = temp;
        render(currentArr)
      }
    }, false)
  </script>