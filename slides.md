---
# try also 'default' to start simple
theme: dracula
class: "text-center"
# https://sli.dev/custom/highlighters.html
lineNumbers: true
# some information about the slides, markdown enabled
info: |
  ## ChatBLT slides via Slidev

  Learn more at [Sli.dev](https://sli.dev)
# page transition
transition: slide-left
---

# ChatBLT

### 🥓🥬🍅

The Amazing AI Chat program that isn't listening to you and only wants to talk about sandwiches.

<!--
quick demo of ChatGPT vs. ChatBlT
-->

---

# Why ChatBLT?

### 🥓🥬🍅

Playing around with ChatGPT got me thinking about the realities of human communication, both text-based an IRL. People often misunderstand each other, don't listen well, etc. So I had the idea to create a "chatbot" that's basically a tech bro mainsplaining something to you at a party and not listening to your side of the conversation at all.

Then I wanted to come up with a cleverish name that sounded kind of like ChatGPT, ideally some acronym that also ended with a T. I landed on ChatBLT, which I decided stood for Bad Listener Tom. But also Bacon Lettuce Tomato. Originally I thought the AI would drone on about all kinds of things like crypto and keto and Joe Rogan, but then, with some nudging from Jaime :), I decided he should stick to sandwiches

<!--
Here is another comment.
-->

---

# Planning Goals

### 🥓🥬🍅

## To Dos

- Rough dupe of ChatGPT intro page
- Form that consists of a single text input and button, and can be submitted via the return key
- comment list component that displays the users input, followed by the "AI response" (randomized string from an array)
- text animation on each new response
- ability to reset state and start new conversation via a button (non-critical stretch goal)

## Stack

- React + TypeScript + CSS Modules via my Next.js boilerplate

---

# Some Fun I Had Along the Way

Fun with loops!

```ts {all|16|18-20}
import { getRandomWordFromArray } from "./string";

const phraseBank: string[] = [
  `Actually, it's pronounced ciabatta`,
  `Actually, it's pronounced aioli`,
  `I have a lot of BLT NFTs. You should have bought in on the ground floor.`,
];

export const getAiResponse = (
  previousPhrase: string | undefined,
  phrases: string[] = phraseBank
): string => {
  if (phrases.length < 2) {
    return phrases[0];
  }
  let responsePhrase = getRandomWordFromArray(phrases);
  //regenerate phrase if it matches the previous one
  while (responsePhrase === previousPhrase) {
    responsePhrase = getRandomWordFromArray(phrases);
  }
  return responsePhrase;
};
```

---

And here's how I tested that

```ts {all|7-11}
describe("AI response utility", () => {
  const chance = new Chance();
  const mockPhrases: string[] = Array.from(Array(2)).map(() =>
    chance.sentence()
  );

  it("should return a string that does not match the previous string", () => {
    expect(getAiResponse(mockPhrases[0], mockPhrases)).not.toEqual(
      mockPhrases[0]
    );
  });

  it("should return a string if the previous string is undefined", () => {
    expect(getAiResponse(undefined, mockPhrases)).toBeTruthy();
  });

  it("should return the only string from an array with a length of one", () => {
    const singlePhrase: string[] = [chance.sentence()];
    expect(getAiResponse(undefined, singlePhrase)).toEqual(singlePhrase[0]);
  });
});
```

---

Fun with custom hooks!

```ts {all|2-4|7-21|23}
export const useAnimateText = (text: string, interval: number = 300) => {
  const [animatedComment, setAnimatedComment] = useState<string>("");
  const [wordCounter, setWordCounter] = useState<number>(0);
  const [isActivelyAnimating, setIsActivelyAnimating] =
    useState<boolean>(false);
  useEffect(() => {
    const commentStrings: string[] = text.split(" ");
    const timer = setTimeout(() => {
      if (wordCounter < commentStrings.length) {
        setIsActivelyAnimating(true);
        const firstWord: string = commentStrings[wordCounter];
        const secondWord: string | undefined =
          commentStrings[wordCounter + 1] ?? "";
        //render text two words at a time
        setAnimatedComment(`${animatedComment} ${firstWord} ${secondWord}`);
        setWordCounter(wordCounter + 2);
      } else {
        setIsActivelyAnimating(false);
      }
    }, interval);
    return () => clearTimeout(timer);
  });
  return { animatedComment, isActivelyAnimating };
};
```

---

Here's how it gets called in the component:

```ts {all|6|7|8}
export const CommentCard: React.FC<PropsType> = ({
  commentData,
  isAnimated = false,
}) => {
  const { comment, author } = commentData;
  const { animatedComment, isActivelyAnimating } = useAnimateText(comment);
  const displayComment: string = isAnimated ? animatedComment : comment;
  const showCursor: boolean = isActivelyAnimating && isAnimated;

  const isUserComment: boolean = author === CommentAuthorTypeMap.USER;
  const cardStyles: string = isUserComment
    ? `${styles.commentCard} ${styles.backgroundLight}`
    : styles.commentCard;
  const avatarWrapperStyles: string = isUserComment
    ? styles.avatarWrapper
    : `${styles.avatarWrapper} ${styles.backgroundTeal}`;
  const icon: ReactNode = isUserComment ? (
    <User height={20} width={20} />
  ) : (
    <EmotionNormal height={20} width={20} />
  );
  return (
    <li className={cardStyles}>
      <div className={styles.commentInner}>
        <div className={avatarWrapperStyles}>{icon}</div>
        <p>
          {displayComment} {showCursor && <span className={styles.cursor} />}
        </p>
      </div>
    </li>
  );
};
```

---

# What I'm proud of

Lighthouse score! 100 in all categories

---

# Next time

Try using the real ChatGPT stream??
