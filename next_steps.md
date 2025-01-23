# Replication Project

- Idea: Replicate the what the paper of the three parts:

1. AI agents "memorize" its simulated counter part
2. AI interviewer who can perform semi-structured interview based on a set of questions
3. AI agents to perform a game and a survey
4. compare the human counter part game/survey result with the AI agents


## Breakdown
1. AI agents "memorize" its simulated counter part
    - code provided in the git
    - important to understand the architecture of the agenet

2. AI interviewer who can perform semi-structured interview based on a set of questions (key)
    - need to see what are the structure to create such AI agent
    - interview script: a json file (table 7)
    - Audio recognision
        - OpenAI Whisper model
        - audio calibration (read aloud first two lines of The Great Gatsby)
    - generate reflections
        - with GPT-4o using following prompt
        ```
        Here is a conversation between an interviewer and an interviewee.
        <INPUT: The transcript of the most recent part of the
        conversation>
        Task: Succinctly summarize the facts about the interviewee based
        on the conversation above in a few bullet points -- again, think
        short, concise bullet points.
        ```
    - Generate new questions 
        - with GPT-4o using following prompt (wow)
        ```
        Meta info:
        Language: English
        Description of the interviewer (Isabella): friendly and curious
        Notes on the interviewee: <INPUT: Reflection notes about the
        participant>
        
        Context:
        This is a hypothetical interview between the interviewer and an
        interviewee. In this conversation, the interviewer is trying to
        ask the following question: "<INPUT: The question in the
        interview script>"
        Current conversation:
        <INPUT: The transcript of the most recent part of the
        conversation>
        =*=*=
        Task Description:
        Interview objective: By the end of this conversation, the
        interviewer has to learn the following: <INPUT: Repeat of the
        question in the interview script, paraphrased as a learning
        objective>
        Safety note: In an extreme case where the interviewee
        *explicitly* refuses to answer the question for privacy reasons,
        do not force the interviewee to answer by pivoting to other
        relevant topics.
        Output the following:
        1) Assess the interview progress by reasoning step by step --
        what did the interviewee say so far, and in your view, what would
        count as the interview objective being achieved? Write a short
        (3~4 sentences) assessment on whether the interview objective is
        being achieved. While staying on the current topic, what kind of
        follow-up questions should the interviewer further ask the
        interviewee to better achieve your interview objective?
        2) Author the interviewer's next utterance. To not go too far
        astray from the interview objective, author a follow-up question
        that would better achieve the interview objective.
        ```

    

3. AI agents to perform several game/survey
    - need to find the game and survey 
    - need to build functionality so that the AI agents can read and perform the survey and game

4. compare the human counter part game/survey result with the AI agents