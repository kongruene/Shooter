# Shooter
  //createSprites
 createEdgeSprites();
var Escore=0;

var Pscore=0;

var stage="start";

//left
var f1=createSprite(101,373);
f1.setAnimation("PStand");
f1.scale=2;

//right
var f2=createSprite(299,373);
f2.setAnimation("EStand");
f2.scale=2;
f2.velocityY=-4;
//f2.setCollider("rectangle",0,0,f2.width,f2.height=f2.height+30);

var hit=createSprite(124,190,18,6);
hit.shapeColor=("brown");
hit.setAnimation("Kill");
hit.visible=(false);

//left
var GunF=createSprite(117,352,10,40);
GunF.setAnimation(" PGun ");
GunF.visible=(false);

//right
var EGunF=createSprite(272,352,10,40);
EGunF.setAnimation(" EGun ");
EGunF.visible=(false);

function draw() {
  //backGround
  background("powderblue");
  f1.velocityX=0;
  
 /* hit.isTouching(f1);
   hit.isTouching(f2);*/
 
   
 if(stage==="start") {
  textFont("monospace");
  fill("purple");
  textAlign(CENTER);
  text("Press Space To Start, press 'S' to shoot, Good luck!",200,150);
  f1.velocityY=0;
  f2.velocityY=0;
 }
  textFont("ink free");
  textAlign(LEFT);
  fill("darkblue");
  text("K.O. "+Pscore,10,20);
  fill("red");
  text("K.O. "+Escore,350,20);
  
  for(var i=0;i<400;i=i+10){
    line(200,i+20,200,i+20);
  }
  if(keyWentDown("space")&&stage==="start"){
    playSound( "sound://category_female_voiceover/go_female.mp3",false);
  }
  //start
  if(keyWentDown("space")&&(stage==="start"||(stage==="f2S"&&(hit.isTouching(f1)||hit.x<0)))){ 
    f2.velocityY=4;
    stage="f1S";
  }
  if(hit.isTouching(f1)&&stage==="f2S"&&hit.velocityX===0){
    Escore=Escore+0;
  }
  if(stage==="f1S"){
    f1.velocityY=0;
    f1.y=199;
    f2.scale=1.25;
    f1.setAnimation("PStandS");
   GunF.y=f1.y;
   EGunF.visible=false;
   f2.setAnimation("EStand");
    hit.visible=(true);
    GunF.visible=(true);
   hit.setAnimation("Kill");
  
    if(keyDown("s")){
      hit.velocityX=9;
    }
   
  }
     if(hit.isTouching(f2)&&stage==="f1S"){
      if(hit.velocityX>0){
      Pscore+=1;
      playSound( "sound://category_achievements/melodic_win_6.mp3",false);
      }
      fill("blue");
      textFont("ink free");
      textSize(30);
      textAlign(CENTER);
      text("HIT!",200,200);
      f2.velocityY=0;
      f2.setAnimation("ELost");
      f2.scale=1.75;
      hit.velocityX=0;
      //hit.x=800;
      f2.setCollider("rectangle", 0, 0, f2.width, 90);
    }
    if(hit.x<0){
      fill("blue");
      textAlign(CENTER);
      textSize(30);
      textFont("ink free");
      text("MISS!",200,200);
      //playSound( "sound://category_achievements/melodic_win_6.mp3",false);
    }
    if((hit.isTouching(f1))&&stage==="f2S"){
      if(hit.velocityX<0){
      Escore+=1;
     playSound( "sound://category_digital/failure.mp3",false);
      }
      f2.velocityY=0;
      f2.setAnimation("ELost");
      f2.scale=1.75;
      hit.velocityX=0;
      //hit.x=800;
    }
  if((hit.isTouching(f2)||hit.x>400)&&stage==="f1S"){
      f2.velocityY=0;
      textAlign(CENTER);
      text("Press space to start",200,160);
    EGunF.visible=(false);
    //hit.x=800;
    }
  if((hit.isTouching(f2)||hit.x>400)&&(stage==="f1S"&&keyDown("space"))){
      stage="f2S";
      hit.x=268;
    }
   if(stage==="f2S"){
    f1.velocityY=0;
    f1.setAnimation("PStand");
    f2.setAnimation("EStandS");
    f1.scale=1.25;
    EGunF.y=f2.y;
    f2.y=200;
    hit.setAnimation("EKill");
    EGunF.visible=(true);
    GunF.visible=(false);
    hit.visible=(true);
    if(hit.x>400){
    hit.velocityX=0;
    }
  if(f1.y===255&&f1.velocityY===-4){
  hit.velocityX=-9;
     }
  
  if(keyDown("up")){
    f1.velocityY=-4;
  }
  if(keyDown("down")){
    f1.velocityY=4;
  }

   // console.log(hit.y);
    }

  if((hit.isTouching(f1))&&stage==="f2S"){
    if(hit.isTouching(f1)){
    f1Shot();
    hit.velocityX=0;
    textAlign(CENTER);
    text("Press space to start",200,160);
    fill("red");
    textFont("ink free");
    textSize(30);
    text("HIT",200,200);
    if(keyDown("space")){
      stage="f1S";
    }
  }
  
  if(Escore===5){
    playSound( "sound://category_male_voiceover/mission_failed_male.mp3",false);
    stage="Lost";
    Pscore=Escore=0;
  }
  }
   if(stage==="Lost"){
     f1.visible=false;
     EGunF.visible=false;
     hit.visible=false;
     f2.setAnimation("EVictor");
     f2.x=200;
     f2.y=200;
     background("rgb(255,204,203)");
     fill("Red");
     textAlign(CENTER);
     textSize("30");
     text("LOST",200,125);
   }

  if((hit.isTouching(f1))&&stage==="f2S"){
    //stage="f1S" ;
    GunF.y=f1.y;
    f2.setAnimation("EStand");
    f1.setAnimation("PLost");
    f1.scale=1.75;
    EGunF.visible=(false);
    f2.velocityY=-4;
    //hit.x=125; 
  }
 // if(f1.setAnimation("PLost")&&stage==="f2S"){
  //  hit.x=125;}
    
  if(hit.x<0){
    textAlign(CENTER);
    fill("blue");
    textFont("ink free");
    textSize(30);
    textAlign(CENTER);
    text("Press space to start",200,160);
    if(keyDown("space")){
      stage="f1S";
      hit.x=GunF.x; 
      hit.velocityX=0; 
    }
  }
  
  if(hit.x>f2.x&&stage==="f1S"&&hit.x>400){
    textAlign(CENTER);
    fill("red");
    textFont("ink free");
    textSize(30);
    text("MISS",200,200);
    hit.velocityX=0;
    }
    
    console.log(World.frameRate);
     
    if(f1.y===255&&f1.velocityY===-4){
    hit.velocityX=-9;
    }
   if((f1.y===139||f1.y===140.75)&&f1.velocityY===4){
    hit.velocityX=-9;
    }
  //GunF.y=f1.y;
  
  if(Pscore===5){
    stage="Win";
    GunF.visible=false;
    hit.visible=false;
    playSound( "sound://category_male_voiceover/objective_achieved_male.mp3",false);
    f1.x=200;
    f1.y=200;
    Pscore=Escore=0;
  }
  
  if(stage==="Win"){
    f1.setAnimation("PVictor");
    f2.visible=false;
    textSize(30);
    background("gold");
    fill("blue");
    text("Win", 200, 125);
  }
  
  
  f1.bounceOff(edges);
  f1.isTouching(f2);
  f2.isTouching(f1);
  f2.bounceOff(edges);
textFont("ink free"); 
  fill(rgb(45.82, 79.92, 143.51));
  textSize(30);
  textAlign(LEFT);
  text("SHOOTER",125,36);
  drawSprites();
}
function f1Shot(){
    f1.velocityY=0;
    f2.scale=1.25;
    /*f1.scale=1.55;
    f1.setAnimation("PLost");*/
   //GunF.y=f1.y;
    hit.visible=(true);
    hit.velocityX=0;
    //GunF.visible=(true);
}
