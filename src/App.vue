<template>
  <div>
    <h3 class="text-center mt-5">เกมเป่ายิงฉุบ</h3>

    <div class="box-game d-flex justify-content-center mt-5">
      <div class="user1">
        <h5 class="text-center">ผู้เล่น 1</h5>
        <img :src="player1ChoiceImage" alt="">
      </div>

      <div class="user2">
        <h5 class="text-center">ผู้เล่น 2</h5>
        <img :src="player2ChoiceImage" alt="">
      </div>
    </div>

    <div class="button mt-5 d-flex justify-content-center">
      <button class="btn btn-danger" @click="playGame"  data-bs-toggle="modal" data-bs-target="#exampleModal">เกมเป่ายิงฉุบ</button>
      <button @click="Resetgame" class="btn btn-success mx-4">เริ่มใหม่</button>
    </div>
  </div>

  <div class="score mt-3 d-flex justify-content-center">
    <div class="d-flex justify-content-center bg-success p-2 text-dark bg-opacity-25 ">

      <p class="fs-5"> คะแนน {{ scorePlayer1 }} : {{ scorePlayer2 }}</p>
    </div>
</div>




    <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5 text-center" id="exampleModalLabel">ผล</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
      <p class="text-center fs-5 fw-bold text-danger">{{ resultMessage }}</p>
      <img :src="imagesplayer" width="300" height="300">
      </div>
     
    </div>
  </div>
</div>

</template>

<script>
export default {
  data() {
    return {
      choices: ['ค้อน', 'กระดาษ', 'กรรไกร'],
      player1Choice: '',
      player2Choice: '',
      player1ChoiceImage: 'https://i.pinimg.com/236x/3d/a9/74/3da974d22ea0b67c84e1738ecd199c1a.jpg', // รูปเริ่มต้น
      player2ChoiceImage: 'https://i.pinimg.com/736x/4a/5b/8f/4a5b8f4db4524bc6b0161fbf00da6564.jpg', // รูปเริ่มต้น
      resultMessage: '',
      scorePlayer1: 0, // คะแนนผู้เล่น 1
      scorePlayer2: 0,  // คะแนนผู้เล่น 2
      
    };
  },
  methods: {
    playGame() {
      const randomIndex1 = Math.floor(Math.random() * this.choices.length);
      const randomIndex2 = Math.floor(Math.random() * this.choices.length);

      this.player1Choice = this.choices[randomIndex1];
      this.player2Choice = this.choices[randomIndex2];

      this.player1ChoiceImage = this.getImagePath(this.player1Choice);
      this.player2ChoiceImage = this.getImagePath(this.player2Choice);

      this.calculateWinner();
    },
    getImagePath(choice) {
      if (choice === 'ค้อน') {
        return 'https://dx.lnwfile.com/_/dx/_raw/cp/z3/u1.jpg';
      } else if (choice === 'กระดาษ') {
        return 'https://static.wixstatic.com/media/249f63_a90293220fb44aa297ad70e06182ed46~mv2.png/v1/fill/w_625,h_469,al_c,q_85,usm_0.66_1.00_0.01,enc_auto/249f63_a90293220fb44aa297ad70e06182ed46~mv2.png';
      } else if (choice === 'กรรไกร') {
        return 'https://image.makewebeasy.net/makeweb/m_1920x0/e8kyJI8FV/scissors/A300.jpg?v=202305101549';
      }
    },
    calculateWinner() {
      if (this.player1Choice === this.player2Choice) {
        this.resultMessage = 'เสมอ';
        this.imagesplayer = "https://i.pinimg.com/236x/bb/df/12/bbdf126c4fba50ebcf7ab8c9c84a8b86.jpg"
      } else if (this.player1Choice ==="ค้อน" && this.player2Choice === "กรรไกร" || 
      this.player1Choice ==="กรรไกร" && this.player2Choice === "กระดาษ" ||
       this.player1Choice ==="กระดาษ" && this.player2Choice === "ค้อน"  ) {
        this.resultMessage = 'ผู้เล่น 1 ชนะ';
        this.scorePlayer1++; // เพิ่มคะแนนผู้เล่น 1
        this.imagesplayer ='https://i.pinimg.com/236x/3d/a9/74/3da974d22ea0b67c84e1738ecd199c1a.jpg';
      } else {
        this.resultMessage = 'ผู้เล่น 2 ชนะ';
        this.scorePlayer2++; // เพิ่มคะแนนผู้เล่น 2
        this.imagesplayer ='https://i.pinimg.com/736x/4a/5b/8f/4a5b8f4db4524bc6b0161fbf00da6564.jpg';
        
      }
    },
      Resetgame(){
        window.location.reload(); // รีเซ็ตหน้าเว็บ
      }
    
    }
  
};
</script>

<style>
.user1,.user2{
  border: 2px solid rgb(227, 12, 12);
  padding: 50px;
}
.box-game img{
  width: 250px;
  height: 250px;
}


</style>