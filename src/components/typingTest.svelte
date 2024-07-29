<script>
  // @ts-ignore
  import { onMount } from "svelte";
  import { faker } from '@faker-js/faker';
  import { createEventDispatcher } from 'svelte';
  import ResultPage from "./resultPage.svelte";

    let text = faker.lorem.paragraph(15);
    let userInput = "";
    let timer = 60 ;
    let interval = 0;
    let correctChars = 0 ;
    let totalChars = 0 ;
    let timeStarted = false;
    let showResult  = false ;
    let wpm  = 0;
    let accuracy = 0;
    const dispatch = createEventDispatcher();


    function startTimer(){
        interval = setInterval(() => {
            timer--;
            if(timer <= 0){
                showResult = true;
                clearInterval(interval);
                caluclateResult();
            }
        },1000)
    }

    // @ts-ignore
    function handleInput(event){
        userInput = event.target.value;
        if(!timeStarted && userInput.length >= 0){
            timeStarted = true;
            startTimer();
        }
        compareInput();
    }

    function compareInput(){
        correctChars = 0 ;
        totalChars = userInput.length;
        for(let i = 0 ; i < userInput.length ; i++){
            if(userInput[i] == text[i]){
                correctChars++;
            }
        }
    }

    
    function caluclateResult(){
        wpm = (correctChars / 5 );
        accuracy = (correctChars / totalChars) * 100;

        alert(`wpm ${wpm}, Accuracy : ${accuracy.toFixed(2)}%`);
        clearType();
    }
    function getHighlightedText(){
        const correctText = text.slice(0,correctChars);
        const incorrectText = text.slice(correctChars,totalChars);
        const remainingText = text.slice(totalChars);
        
        return {correctText , incorrectText , remainingText};
    }

    function clearType(){
        userInput = "";
        timer = 60 ;
        correctChars = 0;
        totalChars = 0;
    }
    
 
    
    
</script>





<div class="testingApp">
    
    <h2>Typing Test</h2>
    
    
    
    {#if showResult}
    <ResultPage wpm={wpm} accuracy={Number(accuracy.toFixed(2))} />
    {:else}
    <div class="logic">
        <div class="inputText">
             <p>{text}</p>
        </div>
            <textarea placeholder="Type Here to Check out Your Typing Skills" bind:value={userInput} on:input={handleInput}/>
        </div>
        <p class="timer">
           Time Left : {timer} seconds
        </p>
         <p class="chars">
            Correct Chars : {correctChars} / Totoal Chars : {totalChars}
        </p>
    {/if}



</div>



<style>

    h2{
        text-align: center;
        letter-spacing: 1.5px;
    }

    .logic{
        display: flex;
        gap: 15px;
    }

    .testingApp{
        display: flex;
        flex-direction: column;
        gap: 20px;
    }

    textarea{
        width: 40vw;
        height: 40vh;
        padding: 5px;
        border-radius: 5px;
        font-size: 15px;
        background-color :burlywood;
        border: 0;
        inset: 0;
        outline: 0ch;
    }

    .timer{
        font-size: 25px;
    }

    .chars{
        font-size: 25px;
    }

    span .correctText{
        color: blue;
    }

</style>