<template>
  <div ref="background_div" class="background_div position-absolute"></div>
  <div ref="endModal" style="display: none; z-index:99; left: 50%; top: 50%; position: fixed; transform: translate(-50%, -50%)">
    <div class="d-flex bg-body flex-column align-items-center justify-content-center  rounded-4 p-5 border-2 border-black">
      <h2>Вы успешно справились с заданиями!</h2>
      <div ref="btn" class="btn mt-3" @click="gameReload">Начать заново</div>
    </div>
  </div>
  <iframe ref="iframe" id="gameFrame" style="position: absolute; z-index: 99; width: 100vw; height: 100vh; display: none; border: none; transition: 1s;"></iframe>
  <div ref="btn" class="btn" style="position: absolute; z-index: 99; right: 1rem; top: 1rem; display: none" @click="closeIframe">Закрыть</div>
</template>


<script>
export default {
  props:{
    images:{
      type: Object,
      required: true,
    }
  },

  data(){
    return {
      endGame: 0
    }
  },

  methods: {
    // Функции по созданию картинок и управления пальчиками
    startGame(){
      this.images.forEach((item) => {
        this.element = this.createItem(item);
        this.$refs.background_div.appendChild(this.element);
      });

      this.giveStart();
    },

    gameReload(){
      window.location.reload();
    },

    createItem(item){
      this.element = document.createElement("img")
      this.element.src = item.src
      this.element.alt = item.alt
      this.element.className = item.className
      this.element.style.zIndex = item.zIndex
      this.element.item_move = item.item_move
      this.element.style.position = "absolute"

      item.width ? this.element.style.width = item.width : '';

      if(item.style_left){
        this.element.style.left = item.style_left + "vh"
      }else if (item.style_right){
        this.element.style.right = item.style_right + "vh"
      }

      if(item.style_top){
        this.element.style.top = item.style_top + "vh"
      }else if(item.style_bottom){
        this.element.style.bottom = item.style_bottom + "vh"
      }

      return this.element
    },

    giveStart(){
      document.querySelector("img.typewriter")?.addEventListener("click", () => {
        this.$refs.iframe.src = 'http://sorter.sfera.local/game/7';
        setTimeout(()=> {
          this.$refs.iframe.style.display = 'block';
          this.$refs.btn.style.display = "block";
          document.querySelector("img.typewriter").style.animation = 'none';
          document.querySelector("img.typewriter").style.filter = 'none';
        }, 200)
        //Печатная машинка - Сортер Было Стало
      })
      document.querySelector("img.chancellery")?.addEventListener("click", () => {
        this.$refs.iframe.src = 'http://memo.sfera.local/';
        setTimeout(()=> {
          this.$refs.iframe.style.display = 'block';
          this.$refs.btn.style.display = "block";
          document.querySelector("img.chancellery").style.animation = 'none';
          document.querySelector("img.chancellery").style.filter = 'none';
        }, 200)
        //Канцелярия - Мемо
      })
      document.querySelector("img.screen")?.addEventListener("click", () => {
        this.$refs.iframe.src = 'http://document.doy.sfera.local/';
        setTimeout(()=> {
          this.$refs.iframe.style.display = 'block';
          this.$refs.btn.style.display = "block";
          document.querySelector("img.screen").style.animation = 'none';
          document.querySelector("img.screen").style.filter = 'none';
        }, 200)
        //Монитор - Исправить ошибки в документе 
      })
      document.querySelector("img.telephone")?.addEventListener("click", () => {
        this.$refs.iframe.src = 'http://situations.sfera.local/game/8';
        setTimeout(()=> {
          this.$refs.iframe.style.display = 'block';
          this.$refs.btn.style.display = "block";
          document.querySelector("img.telephone").style.animation = 'none';
          document.querySelector("img.telephone").style.filter = 'none';
          document.querySelector("img.telephone").style.transform = 'scaleX(-1)';
        }, 200)
        //Телефон - Телефонный разговор
      })
      document.querySelector("img.chair")?.addEventListener("click", () => {
        this.$refs.iframe.src = 'http://checkroom.sfera.local';
        setTimeout(()=> {
          this.$refs.iframe.style.display = 'block';
          this.$refs.btn.style.display = "block";
          document.querySelector("img.chair").style.animation = 'none';
          document.querySelector("img.chair").style.filter = 'none';
        }, 200)
        //Стул - Имидж
      })
      document.querySelector("img.documentsInWardrobe")?.addEventListener("click", () => {
        this.$refs.iframe.src = 'http://chain.doy.sfera.local/';
        setTimeout(()=> {
          this.$refs.iframe.style.display = 'block';
          this.$refs.btn.style.display = "block";
          document.querySelector("img.documentsInWardrobe").style.animation = 'none';
          document.querySelector("img.documentsInWardrobe").style.filter = 'none';
        }, 200)
        //Стопка с папками - Цепочка ДОУ
      })
    },

    closeIframe(){
      this.$refs.iframe.style.display = 'none';
      this.$refs.btn.style.display = "none";
      this.$refs.iframe.src = '';
      this.endGame ++;
    },

    endGameModal(){
      this.$refs.background_div.style.filter = 'blur(5px)'
      this.$refs.endModal.style.display = 'block';
    }
  },

  watch:{
    images(value){
      if (value.length > 0) {
        this.startGame()
      }
    },

    endGame(value){
      if(value === 6) {
        this.endGameModal()
      }
    }
  }
}
</script>

<style>
    .background_div{
      position: relative;
      width: 100%;
      height: 100%;
      display: flex;
      z-index: 1;
      overflow: hidden;
      transition: 1s;

      touch-action: none;
    }

    img.chancellery,
    img.chair,
    img.documentsInWardrobe,
    img.typewriter{
      cursor: pointer;
      filter: drop-shadow(0 0 20px rgba(255, 183, 0));
      border-radius: .2rem;
      animation: pulse 1s infinite alternate-reverse;
    }

    img.telephone{
      rotate: 9deg;
      cursor: pointer;
      filter: drop-shadow(0 0 20px rgba(255, 183, 0));
      border-radius: .2rem;
      animation: pulseThree 1s infinite alternate-reverse;
    }

    img.screen{
      cursor: pointer;
      filter: drop-shadow(0 0 20px rgba(255, 183, 0));
      border-radius: .2rem;
      animation: pulseTwo 1s infinite alternate-reverse;
    }

    @keyframes pulse{
      0% {
        transform: scale(1);
      }
      100% {
        transform: scale(1.05);
      }
    }

    @keyframes pulseTwo{
      0% {
        transform: scaleX(1);
      }
      100% {
        transform: scaleX(1.05);
      }
    }

    @keyframes pulseThree{
      0% {
        transform: scaleX(1) scaleX(-1);
      }
      100% {
        transform: scaleX(1.05) scaleX(-1);
      }
    }


    .btn{
      font-size: 2rem;
      font-weight: 600;
      font-family: Montserrat, sans-serif;
      border: 2px white solid;
      color: white;
      background: #0d7743;
    }

    .btn:hover{
      font-size: 2rem;
      font-weight: 600;
      font-family: Montserrat, sans-serif;
      border: 2px white solid;
      color: white;
      background: #0d7743;
    }
</style>