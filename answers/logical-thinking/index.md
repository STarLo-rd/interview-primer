**1. The Light Bulb Switches Problem**

_Problem:_

You are in a room with three light switches. Each switch controls one of three light bulbs in the adjacent room, but you don't know which switch corresponds to which bulb. You can manipulate the switches as much as you want, but you may only enter the room with the bulbs once. How can you determine which switch controls which bulb?

_Solution:_

1. Turn on the first switch and leave it on for about 10 minutes.
2. After 10 minutes, turn off the first switch and immediately turn on the second switch.
3. Now, enter the room with the bulbs.

- The bulb that is on corresponds to the second switch (since it's currently receiving power).
- The bulb that is off but warm corresponds to the first switch (it was on long enough to heat up and was turned off just before entering the room).
- The bulb that is off and cold corresponds to the third switch (it was never turned on).

**2. The Two Ropes Burning Problem**

_Problem:_

You have two ropes of varying thicknesses and materials. Each rope takes exactly one hour to burn from one end to the other. However, the ropes do not burn at a uniform rate; for example, half the rope could burn in 5 minutes, and the remaining half could take 55 minutes. With these two ropes and a way to light them, how can you measure exactly 45 minutes?

_Solution:_

1. Light both ends of the first rope simultaneously and one end of the second rope at the same time.
2. The first rope will take 30 minutes to burn completely when lit from both ends.
3. At the moment the first rope finishes burning (which is 30 minutes in), light the other end of the second rope.
4. Since the second rope has been burning from one end for 30 minutes, it has 30 minutes of burn time left. Lighting the other end will cause it to burn in half the time, which is 15 minutes.

By adding the 30 minutes from the first rope and the 15 minutes from the second rope, you get a total of 45 minutes.

**3. The Heaven or Hell Door Problem**

_Problem:_

You stand before two doors. One leads to Heaven, and the other leads to Hell. Two guardians are present: one always tells the truth, and the other always lies. You don't know which guardian is which, and you can ask only one question to one of the guardians to determine the door to Heaven. What question do you ask?

_Solution:_

Ask either guardian: "If I were to ask the other guardian which door leads to Heaven, which door would they point to?"

- If you ask the truth-telling guardian, they will truthfully tell you that the other (lying) guardian would point to the Hell door.
- If you ask the lying guardian, they will lie about the truth-teller's response, also pointing to the Hell door.

In both cases, the guardian will indicate the door to Hell. Therefore, you should choose the opposite door to find Heaven.

**4. The Three Boxes Problem**

_Problem:_

You have three boxes: one contains only apples, one contains only oranges, and the third contains both apples and oranges. Each box is labeled, but all labels are incorrect. You are allowed to pick one fruit from one box. How can you label all the boxes correctly?

_Solution:_

1. Choose a fruit from the box labeled "Apples and Oranges." Since all labels are incorrect, this box must contain only apples or only oranges.
2. Suppose you pick an apple. This means the box labeled "Apples and Oranges" contains only apples.
3. The box labeled "Oranges" cannot contain oranges (since its label is incorrect) and cannot contain apples (since we've determined the "Apples and Oranges" box contains only apples). Therefore, it must contain both apples and oranges.
4. The remaining box, labeled "Apples," must contain only oranges.

If you had picked an orange in step 2, the logic would similarly lead you to correctly label all the boxes.

**5. The Monty Hall Problem**

_Problem:_

You're on a game show with three doors. Behind one door is a car; behind the other two are goats. You pick one door. The host, who knows what's behind each door, opens another door, revealing a goat. He then asks if you want to switch your choice to the remaining door or stay with your original choice. What should you do to maximize your chances of winning the car?

_Solution:_

You should switch doors.

When you make your initial choice, there's a 1/3 chance you've picked the car and a 2/3 chance you've picked a goat. When the host reveals a goat behind one of the other two doors, the 2/3 probability doesn't split between the two remaining doors; instead, it remains with the unchosen door. Therefore, switching gives you a 2/3 chance of winning the car, while staying gives you only a 1/3 chance.

These problems are classic examples used to assess logical reasoning and problem-solving skills in technical interviews. Practicing such questions can help you develop a structured approach to tackling complex scenarios, which is invaluable in a backend development role.

**6. The 12 Balls Problem:**

_Problem:_ You have 12 visually identical balls, but one differs in weight (it could be heavier or lighter). Using a balance scale and only three weighings, determine which ball is different and whether it is heavier or lighter.

_Approach:_ Divide the balls into three groups of four. Weigh two groups against each other:

- If they balance, the odd ball is in the third group.
- If they don't, the odd ball is in the heavier or lighter group.

Continue this process, narrowing down the possibilities with each weighing, until you identify the unique ball and its weight difference.

**7. Bridge and Torch Problem:**

_Problem:_ Four people need to cross a bridge at night. They have one torch, and the bridge can hold only two people at a time. Each person walks at a different speed: 1, 2, 5, and 10 minutes respectively. When two people cross together, they move at the slower person's pace. What is the minimum time required for all to cross?

_Approach:_ The optimal strategy involves minimizing the time spent by the two slowest individuals:

1. Person 1 and Person 2 cross (2 minutes).
2. Person 1 returns (1 minute).
3. Person 5 and Person 10 cross (10 minutes).
4. Person 2 returns (2 minutes).
5. Person 1 and Person 2 cross again (2 minutes).

Total time: 2 + 1 + 10 + 2 + 2 = 17 minutes.

**8. Inverted Cards Puzzle:**

_Problem:_ You have 52 cards face down. Exactly 10 of them are face up. You are blindfolded and can flip any cards. How can you split the deck into two piles so that each pile has the same number of face-up cards?

_Approach:_ Divide the deck into two piles of 10 and 42 cards. Flip all the cards in the 10-card pile. Both piles will now have the same number of face-up cards.

These puzzles are designed to assess your logical reasoning and problem-solving skills, which are crucial in software engineering roles. Practicing such questions can enhance your analytical thinking and prepare you for similar challenges in interviews.
