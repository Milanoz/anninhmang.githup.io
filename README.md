<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="/themify-icons/themify-icons.css">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.1/normalize.css">
    <link rel="stylesheet" href="/Quizz/style.css">
    <title>Document</title>
</head>
<body>
    <div class="container" id="quiz">
        <div class="container-top">
            <h3 id="question">Question text</h3>
            <div class="taskbar" id="taskbar">
            </div>
        </div>
        <div class="container-middle">
            <ul>
                <li>
                    <input type="radio" name="answer" id="a" class="answer">
                    <label for="a" id="a_text">answer</label>
                </li>
                <li>
                    <input type="radio" name="answer" id="b" class="answer">
                    <label for="b" id="b_text">answer</label>
                </li>
                <li>
                    <input type="radio" name="answer" id="c" class="answer">
                    <label for="c" id="c_text">answer</label>
                </li>
                <li>
                    <input type="radio" name="answer" id="d" class="answer">
                    <label for="d" id="d_text">answer</label>
                </li>
            </ul>
        </div>
        <div class="container-bottom">
            <button id="submit">Submit</button>
        </div>
    </div>

    <script>

        const quizData = [
            {
                question: "Nguyen Huy la ai:",
                a: "Java",
                b: "Nothing",
                c: "Huy",
                d: "Trứng",
                correct: "a"
            },
            {
                question: "Nguyen Huy la ai123123:",
                a: "Java",
                b: "Nothing",
                c: "Huy",
                d: "Trứng",
                correct: "c"
            },
            {
                question: "Nguyen Huy la ai232323:",
                a: "Java",
                b: "Nothing",
                c: "Huy",
                d: "Trứng",
                correct: "c"
            },
            {
                question: "Nguyen Huy la a232323232i:",
                a: "Java",
                b: "Nothing",
                c: "Huy",
                d: "Trứng",
                correct: "c"
            },
            {
                question: "Nguyen Huy la ai:23232323",
                a: "Java",
                b: "Nothing",
                c: "Huy",
                d: "Trứng",
                correct: "c"
            },
        ]

        const quiz = document.getElementById('quiz');
        const answerEls = document.querySelectorAll('.answer');
        const question = document.getElementById('question');
        const a_text = document.getElementById('a_text');
        const b_text = document.getElementById('b_text');
        const c_text = document.getElementById('c_text');
        const d_text = document.getElementById('d_text');
        const submitBtn = document.getElementById('submit');

        let currentQuiz = 0;
        let score = 0;

        loadQuiz()
        
        function loadQuiz()
        {
            deselectAnswer()

            const currentQuizData = quizData[currentQuiz];

            question.innerText = currentQuizData.question

            a_text.innerText = currentQuizData.a;
            b_text.innerText = currentQuizData.b;
            c_text.innerText = currentQuizData.c;
            d_text.innerText = currentQuizData.d;

        }

        function deselectAnswer()
        {
            answerEls.forEach(answerEl => answerEl.checked = false)
        }

        function getSelected()
        {
            let answer
            answerEls.forEach(answerEls => {
                if (answerEls.checked)
                {
                    answer = answerEls.id
                }
            })
            return answer;
        }

        submitBtn.addEventListener('click', () => {
            const answer = getSelected();
            if (answer)
            {
                if (answer === quizData[currentQuiz].correct)
                {
                    score++;
                }
                currentQuiz++
                if(currentQuiz < quizData.length)
                {
                    loadQuiz()
                }
                else
                {
                    quiz.innerHTML = `
                        <div class="container-bottom">
                            <h2 style="text-align:center;"> Câu hỏi ${score}/${quizData.length} Câu trả lời đúng</h2>
                            <button class="reload" onclick="location.reload()">Làm lại</button>
                        </div>
                    `
                }
            }
            const toTal = document.getElementById('taskbar');
            toTal.innerHTML = `Câu hỏi ${currentQuiz} / ${quizData.length} | Điểm ${score} / ${quizData.length}`;
        })
        

    </script>
</body>
</html>
