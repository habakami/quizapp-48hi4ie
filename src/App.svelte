<script>
    import AnswerButton from "./AnswerButton.svelte";
    import TitlePage from "./TitlePage.svelte";
    import {getQuizdata} from "./quizdataFactory";
    let showTitle = true;
    let currentScore = 0;
    let renzokuSeikai = 0;
    let quizdata = getQuizdata();
    //let quizdata = {mondai: "鮪", seikai: "まぐろ", taku: ["ひらめ", "かれい", "まぐろ", "ぶり", "くじら"]};

    const answerButtonClicked = (isCorrect) => {
        if(isCorrect){
            renzokuSeikai += 1;
            currentScore += renzokuSeikai;
        }
        else{
            renzokuSeikai = 0;
        }
        quizdata = getQuizdata();
    };
</script>

<TitlePage></TitlePage>

<main class="flex flex-col h-dvh">
    <!-- メニューバー -->
    <div class="bg-red-200 flex justify-around text-xl font-bold p-3">
        <div>スコア:{currentScore}</div>
        <div>連続正解数:{renzokuSeikai}</div>
    </div>

    <!-- 問題 -->
    <div class="bg-green-200 text-center text-4xl py-4">{quizdata.mondai}</div>
    
    <!-- 選択肢 -->
    <div class="bg-blue-200 flex flex-col justify-around flex-grow items-center">
        {#each quizdata.taku as t}
            <AnswerButton on:click={() => answerButtonClicked(quizdata.seikai===t)}>{t}</AnswerButton>
        {/each}
    </div>
</main>