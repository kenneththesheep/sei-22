## Project Post Mortem
Post mortems are important to understand about what happened in a project and actively think about what you learned.

Post-mortems are meant to be a blame-less space open to objective conversation about what went well and what could be improved.

Even in the examples below, where tens of millions of dollars could be lost, the best approach is to think through the series of events that led to the outcome.

Large mistakes are almost never the fault of the developer, but of the sytems and processes in place to prevent errors and problems.

[https://github.com/danluu/post-mortems](https://github.com/danluu/post-mortems)
https://blog.codinghorror.com/the-project-postmortem/



### What to Bring
Please answer the following questions. Take at least 30 minutes to prepare.

#### Approach and Process

1. What in my process and approach to this project would I do differently next time?

The process was to build in chunks.
<ol>
	<li>First was to have an idea which was manageable and something which I can relate to. Since I was doing my programming most of the night time and doing daddy duty, therefore the idea came about.</li>
	<li>First was to come up with the controls by collecting the necessary control keys to manipulate different matter</li>
	<li>Next was to create a map using a 2X2 array. I did a fair bit of testing for the boundary, movement, etc.</li>
	<li>Next was to create the variables to manipulate what will happen at each set of coordinates</li>
	<li>Next was to create the game screen, introduction screen. I let my better half look through, criticize and improve upon it.</li>
	<li>DOM the introduction screen and game screen</li>
	<li>Add the other features</li>
</ol>

<br>Important Lessons: <br>
a) I learn the hard way. After I DOM, I happily deleted the html. When my better half look through and told me to adjust, when I tried to do the developer tool, I cannot adjust. I realize the only way to manage is to go to git and copy back the html for manipulation. <br>
b) I went straight in coding and rushing the coding without thinking refactoring. It made the code like a giant hay stack. I know what I should have done. a) Refactoring into a function. b) Label my function and variable. Always good to comment like Section: To update the looks of the stamina gauge. It makes finding the code and documentation faster.<br>
c) Always have a second eye. What seems good to me was quickly dismissed by my better half who is more aesthetically inclined like layout, color scheme, font type, etc.<br>

1. What in my process and approach to this project went well that I would repeat next time?

It was like a series of short sprint and decisions had to be made very quickly. I remembered I had to decide when to do the css (like when my better half is awake) and when to do long process of doming (when everyone is asleep.). <br> I had to make decisive decision like whether to css the map or draw it and set as background. I went for the latter as it is neater in terms of the coding.<br> Searching for the right images and sound tracks was a challenge as I needed to think which image will look good as the background and which sound tracks set the ambiance right( I made those decision as I am more musically inclined than my better half).


#### Code and Code Design

1. What in my code and program design in the project would I do differently next time?<br>
There are a few. As mentioned above, when I code, I tend not to refactor and go straight, causing a large of repeated code. I tidied up after the soft launch with Stuart who rightly pointed out. When I code, I tend to only do refactoring when I tidy up which I know should be the reverse so it makes my life easier. <br>
Another is the naming convention of my variables, functions, selector. A lot of time wasted when I needed to return back to check whether it was variable, function or selector as my names tends to get too close. (Wasn't thinking when I coded. It was a bad habit I had since Poly days where my variables are i, m and j).
Example: (Line 1 to 20)
Section 1: Code

var gameStart = false;
var toggleInstructionSwitch = false;
var toggleControlSwitch = false;
var toggleHelpSwitch = false;
var restart;
var timerIntervalFunction;
var mapStatus = false;
var backgroundMusic = "Music/ElfenLiedLilium.mp3";
var DungeonMusic = "Music/MusicBox.mp3"
var startSound;
var dungeonSound;
var staminaDepletion;
var explodeSound = "SoundEffect/Explode.mp3";
var explode;
var NoStaminaSound = "SoundEffect/NoStamina.wav";
var NoStamina;
var WinSound = "SoundEffect/Win.wav";
var win;
var wrathSound = "SoundEffect/womanwrath.mp3"

Another thing is to add mouse click interface as for now, it is run by keyboard but when on mobile devices, it can load but cannot play.

I also want to look into animation and drag functions. Also to work on canvas

1. What in my code and program design in the project went well? Is there anything I would do the same next time?

I love three parts of my code really well.
One is the portion is the updating of stamina. It took me a while to figure how to shift the css so it will always remain relatively to the center especially, the shape is not a circle and I cannot simply use margin:0 auto.
<!--Section 7-->
Section 7 Code:

var staminaDistanceCheck=function(m){
    var displayStamina = document.getElementById("staminaCount");
    if(player.stamina === 100)
    {

        displayStamina.style.marginLeft = "18px";
    }
    else if(player.stamina > 9 && player.stamina < 100)
    {
        if(m.matches){
            console.log("matches");
            displayStamina.style.marginLeft = "9px";
        }
        else{
                displayStamina.style.marginLeft = "25px";
            }
    }
    else
    {
        if(m.matches){
            console.log("matches");
            displayStamina.style.marginLeft = "15px";
        }
        else
        {
            displayStamina.style.marginLeft = "35px";
        }
    }
}

The other is the background music and sound effect. I really learn a lot. I realize not everything is setAttribute. Some things can be just boolean like loop which I console log to find out. Also to manage the play() so it can play well.

Secion 5
//more for music background
function sound(src) {
  this.sound = document.createElement("audio");
  this.sound.src = src;
  this.sound.setAttribute("preload", "auto");
  this.sound.setAttribute("controls", "none");
  this.sound.style.display = "none";
  this.sound.loop=true;
  document.body.appendChild(this.sound);
  this.play = function(){

    this.sound.play();
  }
  this.stop = function(){
    this.sound.pause();
  }
}

Another is the manipulation of the map png files and using the coordinates to display the right map image. I had a foretaste of it in the AJAX exercise but wasn't too sure how to manipulate until this project.

Section 20:
var mapMode = function(){
    console.log("map mode");
    console.log(player.xCoordinate.toString());
    console.log(player.yCoordinate.toString());
    var mapDisplayUrl = "map/map" + player.yCoordinate.toString() + player.xCoordinate.toString() + ".png";
    console.log(mapDisplayUrl);
    console.log(typeof mapDisplayUrl);

    var mapImage = document.getElementById("gamescreen");
    mapImage.style.backgroundImage = `url(${mapDisplayUrl})`;
}



  For each, please include code examples.
  1. Code snippet up to 20 lines.
  2. Code design documents or architecture drawings / diagrams.

#### WDI Unit 1 Post Mortem
1. What habits did I use during this unit that helped me?
I appreciate the further challenges. I remember when I first ask the question whether how can the input accept two entries, I remember the challenge was it is possible and as I was riding back on the bus, it strike upon me to use a switch to go through the different input.<br>

Project management is something I learn a lot, especially on remote and with a kid who is not well at the background. It helped me to work in burst and when I get distracted(most of the time), through the time, I learn to be able to store in my mind where I was and get back pretty quickly after coming back.

2. What habits did I have during this unit that I can improve on?
My coding structure and refactoring should be work upon. I am not very good in memory work so from time to time, I refer back. Also, I still struggle with Mac. Never easy to adapt so easily.


3. How is the overall level of the course during this unit? (instruction, course materials, etc.)
Firstly, because of this course, now I am more used to it than windows. When I use back my personal laptop, I messed up the controls as all the controls are inverted compare to mac.

I think though the homework is quite relentless (:) ) I really benefited from it as I am more of a kinesthetic learner. I learn best when I do something. To be honest, I was not looking at the notes for the homework but when it was the project, I really benefited from it. It helps when there is an open Q&A as that is the time where I actually learn. 