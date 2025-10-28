# react official website teaching assignments

## Describing the UI

### Passing Props to a Component 将 Props 传递给组件

#### challenge 1:

```
function getImageUrl(imageId, size = 's') {
    return (
        'https://i.imgur.com/' +
        imageId +
        size +
        '.jpg'
    );
}


function Profile({
                     sectionClassname = "profile",
                     name,
                     imgClassName = "avatar",
                     imgSrc,
                     imgAlt,
                     profession,
                     AwardsNumber,
                     AwardsName,
                     Discovered
                 }) {
    return (
        <section className={sectionClassname}>
            <h2>{name}</h2>
            <img
                className={imgClassName}
                src={getImageUrl(imgSrc)}
                alt={imgAlt}
                width={70}
                height={70}
            />
            <ul>
                <li>
                    <b>Profession: </b>
                    {profession}
                </li>
                <li>
                    <b>Awards: {AwardsName.length} </b>
                    ({AwardsName})
                </li>
                <li>
                    <b>Discovered: </b>
                    {Discovered}
                </li>
            </ul>
        </section>
    );
}

export default function Gallery() {
    return (
        <div>
            <h1>Notable Scientists</h1>
            <Profile name={"Maria Skłodowska-Curie"} imgSrc={'szV5sdG'}
                     imgAlt={"Maria Skłodowska-Curie"} profession={"physicist and chemist"} AwardsNumber={4}
                     AwardsName={["Nobel Prize in Physics", "Nobel Prize in Chemistry", "Davy Medal", "Matteucci Medal"]}
                     Discovered={"polonium(chemical element)"}
            />
            <Profile name={"Katsuko Saruhashi"} imgSrc={'YfeOqp2'} imgAlt={"Katsuko Saruhashi"}
                     profession={"geochemist"} AwardsNumber={2}
                     AwardsName={["Miyake Prize for geochemistry", "Tanaka Prize"]}
                     Discovered={"a method for measuring carbon dioxide in seawater"}/>
        </div>
    );
}

```

#### challenge 2:

```
import { getImageUrl } from './utils.js';

function Avatar({ person, size }) {
  let thumbnailSize = 's';
  if (size > 90) {
    thumbnailSize = 'b';
  }
  return (
    <img
      className="avatar"
      src={getImageUrl(person, thumbnailSize)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <>
      <Avatar
        size={40}
        person={{ 
          name: 'Gregorio Y. Zara', 
          imageId: '7vQD0fP'
        }}
      />
      <Avatar
        size={120}
        person={{ 
          name: 'Gregorio Y. Zara', 
          imageId: '7vQD0fP'
        }}
      />
    </>
  );
}

```



#### challenge 3:

```
function Avatar({title, content, img}) {
    if (img == null) {
        return (
            <div className="card-content">
                <h1>{title}</h1>
                <p>{content}</p>
            </div>);
    } else {
        return (
            <div className="card-content">
                <h1>{title}</h1>
                <img
                    className={img.className}
                    src={img.src}
                    alt={img.alt}
                    width={img.width}
                    height={img.height}
                />
            </div>);
    }
}

function Card({children}) {
    return (
        <div className="card">
            {children}
        </div>
    );
}

export default function Profile() {
    return (
        <div>
            <Card>
                <Avatar
                    title={"Photo"}
                    img={{
                        className : "avatar",
                        src: "https://i.imgur.com/OKS67lhm.jpg",
                        alt: "Aklilu Lemma",
                        width: 70,
                        height: 70
                    }}/>
            </Card>

            <Card>
                <Avatar title={"About"}
                        content={"Aklilu Lemma was a distinguished Ethiopian scientist who discovered a natural treatment to schistosomiasis."}/>
            </Card>
        </div>
    );
}

```

### Conditional Rendering 条件渲染

#### challenge 1:

```
function Item({ name, isPacked }) {
  return (
      <li className="item">
        {isPacked ? name + '✅':name + `❌︎`}
      </li>
  );
}

export default function PackingList() {
  return (
      <section>
        <h1>Sally Ride's Packing List</h1>
        <ul>
          <Item
              isPacked={true}
              name="Space suit"
          />
          <Item
              isPacked={true}
              name="Helmet with a golden leaf"
          />
          <Item
              isPacked={false}
              name="Photo of Tam"
          />
        </ul>
      </section>
  );
}

```

#### challenge 2:

```
function Item({name, importance}) {
    return (
        <li className="item">
            {name} {importance > 0 && (<em>(Importance : {importance})</em>)}
            </li>
            );
        }

export default function PackingList() {
    return (
        <section>
            <h1>Sally Ride's Packing List</h1>
            <ul>
                <Item
                    importance={9}
                    name="Space suit"
                />
                <Item
                    importance={0}
                    name="Helmet with a golden leaf"
                />
                <Item
                    importance={6}
                    name="Photo of Tam"
                />
            </ul>
        </section>
    );
}

```

#### condition 3:

```
function Drink({name}) {
  if (name === 'tea') {
    return (
        <section>
          <h1>{name}</h1>
          <dl>
            <dt>Part of plant</dt>
            <dd>{'leaf'}</dd>
            <dt>Caffeine content</dt>
            <dd>{'15–70 mg/cup'}</dd>
            <dt>Age</dt>
            <dd>{'4,000+ years'}</dd>
          </dl>
        </section>
    );
  }
  if (name === 'coffee') {
    return (
        <section>
          <h1>{name}</h1>
          <dl>
            <dt>Part of plant</dt>
            <dd>{'bean'}</dd>
            <dt>Caffeine content</dt>
            <dd>{'80–185 mg/cup'}</dd>
            <dt>Age</dt>
            <dd>{'1,000+ years'}</dd>
          </dl>
        </section>
    );
  }

}

export default function DrinkList() {
  return (
      <div>
        <Drink name="tea"/>
        <Drink name="coffee"/>
      </div>
  );
}

```

### Rendering Lists 渲染列表

#### challenge 1:

```
function getImageUrl(person) {
    return (
        'https://i.imgur.com/' +
        person.imageId +
        's.jpg'
    );
}

const people = [{
    id: 0,
    name: 'Creola Katherine Johnson',
    profession: 'mathematician',
    accomplishment: 'spaceflight calculations',
    imageId: 'MK3eW3A'
}, {
    id: 1,
    name: 'Mario José Molina-Pasquel Henríquez',
    profession: 'chemist',
    accomplishment: 'discovery of Arctic ozone hole',
    imageId: 'mynHUSa'
}, {
    id: 2,
    name: 'Mohammad Abdus Salam',
    profession: 'physicist',
    accomplishment: 'electromagnetism theory',
    imageId: 'bE7W1ji'
}, {
    id: 3,
    name: 'Percy Lavon Julian',
    profession: 'chemist',
    accomplishment: 'pioneering cortisone drugs, steroids and birth control pills',
    imageId: 'IOjWm71'
}, {
    id: 4,
    name: 'Subrahmanyan Chandrasekhar',
    profession: 'astrophysicist',
    accomplishment: 'white dwarf star mass calculations',
    imageId: 'lrWQx8l'
}];

export default function List() {
    const chemists = people.filter(person => {
        return person.profession === 'chemist';
    });

    const others = people.filter(person => person.profession !== 'chemist')
    const otherListItems = others.map(person =>
        <li key={person.id}>
            <img
                src={getImageUrl(person)}
                alt={person.name}
            />
            <p>
                <b>{person.name}:</b>
                {' ' + person.profession + ' '}
                known for {person.accomplishment}
            </p>
        </li>
    );
    const chemistsListitems = chemists.map(person =>
        <li key={person.id}>
            <img
                src={getImageUrl(person)}
                alt={person.name}
            />
            <p>
                <b>{person.name}:</b>
                {' ' + person.profession + ' '}
                known for {person.accomplishment}
            </p>
        </li>);
    return (
        <article>
            <h1>Scientists</h1>
            <ul>{otherListItems}</ul>
            <h1>Chemists</h1>
            <ul>{chemistsListitems}</ul>
        </article>
    );
}


```

#### challenge 2:

```
export const recipes = [{
    id: 'greek-salad',
    name: 'Greek Salad',
    ingredients: ['tomatoes', 'cucumber', 'onion', 'olives', 'feta']
}, {
    id: 'hawaiian-pizza',
    name: 'Hawaiian Pizza',
    ingredients: ['pizza crust', 'pizza sauce', 'mozzarella', 'ham', 'pineapple']
}, {
    id: 'hummus',
    name: 'Hummus',
    ingredients: ['chickpeas', 'olive oil', 'garlic cloves', 'lemon', 'tahini']
}];

function showRecipes() {
    const a = recipes.map(food => {
        return (<div key={food.id}>
            <h2>{food.name}</h2>
            <ul>{food.ingredients.map(ingredients => {
                return (<li key={ingredients}>{ingredients}</li>);
            })}</ul>
        </div>);
    });
    return a;
}

export default function RecipeList() {
    return (
        <div>
            <h1>Recipes</h1>
            {showRecipes()}
        </div>
    );
}


```

#### challenge 3:

```
const recipes = [{
    id: 'greek-salad',
    name: 'Greek Salad',
    ingredients: ['tomatoes', 'cucumber', 'onion', 'olives', 'feta']
}, {
    id: 'hawaiian-pizza',
    name: 'Hawaiian Pizza',
    ingredients: ['pizza crust', 'pizza sauce', 'mozzarella', 'ham', 'pineapple']
}, {
    id: 'hummus',
    name: 'Hummus',
    ingredients: ['chickpeas', 'olive oil', 'garlic cloves', 'lemon', 'tahini']
}];

function Recipe({id, name, ingredients}) {
    return (
        <div key={id}>
            <h2>{name}</h2>
            <ul>
                {ingredients.map(ingredients => {
                    return (
                        <li key={ingredients}>{ingredients}</li>
                    );
                })}
            </ul>
        </div>
    );
}

export default function RecipeList() {
    return (
        <div>
            <h1>Recipes</h1>
            {recipes.map(recipes => (
                <Recipe key={recipes.id} {...recipes}></Recipe>))}
        </div>
    );
}

```

#### challenge 4:

```
const poem = {
    lines: [
        'I write, erase, rewrite',
        'Erase again, and then',
        'A poppy blooms.'
    ]
};

function poet() {
}

export default function Poem() {
    let output = [];

    poem.lines.forEach((line, i) => {
        output.push(<p key={i + '-text'}> {line} </p>)
        output.push(<hr key={i + 'separator'}/> )
    })
    output.pop();

    return (
        <article>
            {output}
        </article>
    );
}

```

### Keeping Components Pure 保持组件纯净

#### challenge 1:

```
export default function Clock({time}) {
    const hours = time.getHours();
    let className;
    if (hours >= 0 && hours <= 6) {
        className = 'night';
    } else {
        className = 'day';
    }
    return (
        <h1 id={className}>
            {time.toLocaleTimeString()}
        </h1>
    );
}

```

#### challenge 2:

`Profile.js`

```
import Panel from './Panel.js';
import { getImageUrl } from './utils.js';

export default function Profile({ person }) {
  return (
    <Panel>
      <Header person={person}/>
      <Avatar person={person} />
    </Panel>
  )
}

function Header({person}) {
  return <h1>{person.name}</h1>;
}

function Avatar({person}) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={50}
      height={50}
    />
  );
}

```

`App.js`

```
import Profile from './Profile.js';

export default function App() {
  return (
    <>
      <Profile person={{
        imageId: 'lrWQx8l',
        name: 'Subrahmanyan Chandrasekhar',
      }} />
      <Profile person={{
        imageId: 'MK3eW3A',
        name: 'Creola Katherine Johnson',
      }} />
    </>
  )
}

```

#### challenge 3:

```
export default function StoryTray({ stories }) {
    let copyStories = stories.slice();
    copyStories.push({
    id: 'create',
    label: 'Create Story'
  });
  return (
    <ul>
      {copyStories.map(story => (
        <li key={story.id}>
          {story.label}
        </li>
      ))}
    </ul>
  );
}

```

## Adding Interactivity 添加交互性

### Responding to Events 响应事件

#### challenge 1:

```
export default function LightSwitch() {
  function handleClick() {
    let bodyStyle = document.body.style;
    if (bodyStyle.backgroundColor === 'black') {
      bodyStyle.backgroundColor = 'white';
    } else {
      bodyStyle.backgroundColor = 'black';
    }
  }

  return (
    <button onClick={handleClick}>
      Toggle the lights
    </button>
  );
}
```

#### challenge 2:

```
export default function ColorSwitch({
  onChangeColor
}) {
  return (
    <button onClick ={e => {
      e.stopPropagation();
      onChangeColor();
    }} >
      Change color
    </button>
  );
}
```

### State: A Component's Memory 状态：组件的记忆

#### challenge 1:

```
import {useState} from 'react';

export const sculptureList = [{
    name: 'Homenaje a la Neurocirugía',
    artist: 'Marta Colvin Andrade',
    description: 'Although Colvin is predominantly known for abstract themes that allude to pre-Hispanic symbols, this gigantic sculpture, an homage to neurosurgery, is one of her most recognizable public art pieces.',
    url: 'https://i.imgur.com/Mx7dA2Y.jpg',
    alt: 'A bronze statue of two crossed hands delicately holding a human brain in their fingertips.'
}, {
    name: 'Floralis Genérica',
    artist: 'Eduardo Catalano',
    description: 'This enormous (75 ft. or 23m) silver flower is located in Buenos Aires. It is designed to move, closing its petals in the evening or when strong winds blow and opening them in the morning.',
    url: 'https://i.imgur.com/ZF6s192m.jpg',
    alt: 'A gigantic metallic flower sculpture with reflective mirror-like petals and strong stamens.'
}, {
    name: 'Eternal Presence',
    artist: 'John Woodrow Wilson',
    description: 'Wilson was known for his preoccupation with equality, social justice, as well as the essential and spiritual qualities of humankind. This massive (7ft. or 2,13m) bronze represents what he described as "a symbolic Black presence infused with a sense of universal humanity."',
    url: 'https://i.imgur.com/aTtVpES.jpg',
    alt: 'The sculpture depicting a human head seems ever-present and solemn. It radiates calm and serenity.'
}, {
    name: 'Moai',
    artist: 'Unknown Artist',
    description: 'Located on the Easter Island, there are 1,000 moai, or extant monumental statues, created by the early Rapa Nui people, which some believe represented deified ancestors.',
    url: 'https://i.imgur.com/RCwLEoQm.jpg',
    alt: 'Three monumental stone busts with the heads that are disproportionately large with somber faces.'
}, {
    name: 'Blue Nana',
    artist: 'Niki de Saint Phalle',
    description: 'The Nanas are triumphant creatures, symbols of femininity and maternity. Initially, Saint Phalle used fabric and found objects for the Nanas, and later on introduced polyester to achieve a more vibrant effect.',
    url: 'https://i.imgur.com/Sd1AgUOm.jpg',
    alt: 'A large mosaic sculpture of a whimsical dancing female figure in a colorful costume emanating joy.'
}, {
    name: 'Ultimate Form',
    artist: 'Barbara Hepworth',
    description: 'This abstract bronze sculpture is a part of The Family of Man series located at Yorkshire Sculpture Park. Hepworth chose not to create literal representations of the world but developed abstract forms inspired by people and landscapes.',
    url: 'https://i.imgur.com/2heNQDcm.jpg',
    alt: 'A tall sculpture made of three elements stacked on each other reminding of a human figure.'
}, {
    name: 'Cavaliere',
    artist: 'Lamidi Olonade Fakeye',
    description: "Descended from four generations of woodcarvers, Fakeye's work blended traditional and contemporary Yoruba themes.",
    url: 'https://i.imgur.com/wIdGuZwm.png',
    alt: 'An intricate wood sculpture of a warrior with a focused face on a horse adorned with patterns.'
}, {
    name: 'Big Bellies',
    artist: 'Alina Szapocznikow',
    description: "Szapocznikow is known for her sculptures of the fragmented body as a metaphor for the fragility and impermanence of youth and beauty. This sculpture depicts two very realistic large bellies stacked on top of each other, each around five feet (1,5m) tall.",
    url: 'https://i.imgur.com/AlHTAdDm.jpg',
    alt: 'The sculpture reminds a cascade of folds, quite different from bellies in classical sculptures.'
}, {
    name: 'Terracotta Army',
    artist: 'Unknown Artist',
    description: 'The Terracotta Army is a collection of terracotta sculptures depicting the armies of Qin Shi Huang, the first Emperor of China. The army consisted of more than 8,000 soldiers, 130 chariots with 520 horses, and 150 cavalry horses.',
    url: 'https://i.imgur.com/HMFmH6m.jpg',
    alt: '12 terracotta sculptures of solemn warriors, each with a unique facial expression and armor.'
}, {
    name: 'Lunar Landscape',
    artist: 'Louise Nevelson',
    description: 'Nevelson was known for scavenging objects from New York City debris, which she would later assemble into monumental constructions. In this one, she used disparate parts like a bedpost, juggling pin, and seat fragment, nailing and gluing them into boxes that reflect the influence of Cubism’s geometric abstraction of space and form.',
    url: 'https://i.imgur.com/rN7hY6om.jpg',
    alt: 'A black matte sculpture where the individual elements are initially indistinguishable.'
}, {
    name: 'Aureole',
    artist: 'Ranjani Shettar',
    description: 'Shettar merges the traditional and the modern, the natural and the industrial. Her art focuses on the relationship between man and nature. Her work was described as compelling both abstractly and figuratively, gravity defying, and a "fine synthesis of unlikely materials."',
    url: 'https://i.imgur.com/okTpbHhm.jpg',
    alt: 'A pale wire-like sculpture mounted on concrete wall and descending on the floor. It appears light.'
}, {
    name: 'Hippos',
    artist: 'Taipei Zoo',
    description: 'The Taipei Zoo commissioned a Hippo Square featuring submerged hippos at play.',
    url: 'https://i.imgur.com/6o5Vuyu.jpg',
    alt: 'A group of bronze hippo sculptures emerging from the sett sidewalk as if they were swimming.'
}];


export default function Gallery() {
    const [index, setIndex] = useState(0);
    const [showMore, setShowMore] = useState(false);

    function handleNextClick() {
        if (index < sculptureList.length - 1) {
            setIndex(index + 1);
        }
    }

    function handlePreviousClick() {
        if (index > 0) {
            setIndex(index - 1);
        }
    }

    function handleMoreClick() {
        setShowMore(!showMore);
    }

    let sculpture = sculptureList[index];
    return (
        <>
            <button onClick={handleNextClick} disabled={index >= sculptureList.length - 1}>
                Next
            </button>
            <button onClick={handlePreviousClick} disabled={index <= 0}>
                Previous
            </button>
            <h2>
                <i>{sculpture.name} </i>
                by {sculpture.artist}
            </h2>
            <h3>
                ({index + 1} of {sculptureList.length})
            </h3>
            <button onClick={handleMoreClick}>
                {showMore ? 'Hide' : 'Show'} details
            </button>
            {showMore && <p>{sculpture.description}</p>}
            <img
                src={sculpture.url}
                alt={sculpture.alt}
            />
        </>
    );
}

```

#### challenge 2:

```
import {useState} from 'react';

export default function Form() {
    const [strFirstName, setFirstName] = useState("")
    const [strLastName, setLastName] = useState("")

    function handleFirstNameChange(e) {
        setFirstName(e.target.value);
    }

    function handleLastNameChange(e) {
        setLastName(e.target.value);
    }

    function handleReset() {
        setFirstName("");
        setLastName("");
    }

    return (
        <form onSubmit={e => e.preventDefault()}>
            <input
                placeholder="First name"
                value={strFirstName}
                onChange={handleFirstNameChange}
            />
            <input
                placeholder="Last name"
                value={strLastName}
                onChange={handleLastNameChange}
            />
            <h1>Hi, {strFirstName} {strLastName}</h1>
            <button onClick={handleReset}>Reset</button>
        </form>
    );
}

```

#### challenge 3:

```
import { useState } from 'react';

export default function FeedbackForm() {
  const [isSent, setIsSent] = useState(false);
  const [message, setMessage] = useState('');
  if (isSent) {
    return <h1>Thank you!</h1>;
  } else {
    return (
      <form onSubmit={e => {
        e.preventDefault();
        alert(`Sending: "${message}"`);
        setIsSent(true);
      }}>
        <textarea
          placeholder="Message"
          value={message}
          onChange={e => setMessage(e.target.value)}
        />
        <br />
        <button type="submit">Send</button>
      </form>
    );
  }
}

```

#### challenge 4:

```
import { useState } from 'react';

export default function FeedbackForm() {

    function handleClick() {
        const name = prompt('What is your name?');
        alert(`Hello, ${name}!`);
    }

    return (
        <button onClick={handleClick}>
            Greet
        </button>
    );
}a

```

### State as a Snapshot 状态快照

#### challenge 1:

```
import {useState} from 'react';

export default function TrafficLight() {
    const [walk, setWalk] = useState(true);

    function handleClick() {
        setWalk(!walk);
        alert(walk ? 'Stop is next' : 'Walk is next' )
    }

    return (
        <>
            <button onClick={handleClick}>
                Change to {walk ? 'Stop' : 'Walk'}
            </button>
            <h1 style={{
                color: walk ? 'darkgreen' : 'darkred'
            }}>
                {walk ? 'Walk' : 'Stop'}
            </h1>
        </>
    );
}
```

### Queueing a Series of State Updates 将一系列状态更新加入队列

#### challenge 1:

```
import { useState } from 'react';

export default function RequestTracker() {
    const [pending, setPending] = useState(0);
    const [completed, setCompleted] = useState(0);

    async function handleClick() {
        setPending(n => n+ 1);
        await delay(3000);
        setPending(n => n- 1);
        setCompleted(n => n+ 1);
    }

    return (
        <>
            <h3>
                等待：{pending}
            </h3>
            <h3>
                完成：{completed}
            </h3>
            <button onClick={handleClick}>
                购买
            </button>
        </>
    );
}

function delay(ms) {
    return new Promise(resolve => {
        setTimeout(resolve, ms);
    });
}

```

#### challenge 2:

```
function getFinalState(baseState, queue) {
    let finalState = baseState;
    // TODO: 对队列做些什么...
    for (const finalStateElement of queue) {
        if (typeof finalStateElement === 'number') {
            finalState = finalStateElement;
        } else if (typeof finalStateElement === 'function') {
            finalState = finalStateElement(finalState);
        }
    }
    return finalState;
}

function increment(n) {
    return n + 1;
}

increment.toString = () => 'n => n+1';

export default function App() {
    return (
        <>
            <TestCase
                baseState={0}
                queue={[1, 1, 1]}
                expected={1}
            />
            <hr/>
            <TestCase
                baseState={0}
                queue={[
                    increment,
                    increment,
                    increment
                ]}
                expected={3}
            />
            <hr/>
            <TestCase
                baseState={0}
                queue={[
                    5,
                    increment,
                ]}
                expected={6}
            />
            <hr/>
            <TestCase
                baseState={0}
                queue={[
                    5,
                    increment,
                    42,
                ]}
                expected={42}
            />
        </>
    );
}

function TestCase({
                      baseState,
                      queue,
                      expected
                  }) {
    const actual = getFinalState(baseState, queue);
    return (
        <>
            <p>初始 state：<b>{baseState}</b></p>
            <p>队列：<b>[{queue.join(', ')}]</b></p>
            <p>预期结果：<b>{expected}</b></p>
            <p style={{
                color: actual === expected ?
                    'green' :
                    'red'
            }}>
                你的结果：<b>{actual}</b>
                {' '}
                ({actual === expected ?
                '正确' :
                '错误'
            })
            </p>
        </>
    );
}

```



### Updating Objects in State 更新状态中的对象

#### challenge 1:

```
import { useState } from 'react';

export default function Scoreboard() {
  const [player, setPlayer] = useState({
    firstName: 'Ranjani',
    lastName: 'Shettar',
    score: 10,
  });

  function handlePlusClick() {
    setPlayer({
      ...player,
      score : ++player.score,
    });
  }

  function handleFirstNameChange(e) {
    setPlayer({
      ...player,
      firstName: e.target.value,
    });
  }

  function handleLastNameChange(e) {
    setPlayer({
      ...player,
      lastName: e.target.value
    });
  }

  return (
    <>
      <label>
        Score: <b>{player.score}</b>
        {' '}
        <button onClick={handlePlusClick}>
          +1
        </button>
      </label>
      <label>
        First name:
        <input
          value={player.firstName}
          onChange={handleFirstNameChange}
        />
      </label>
      <label>
        Last name:
        <input
          value={player.lastName}
          onChange={handleLastNameChange}
        />
      </label>
    </>
  );
}

```

#### challenge 2:

```
import {useState} from 'react';

export default function Box({
                                children,
                                color,
                                position,
                                onMove
                            }) {
    const [
        lastCoordinates,
        setLastCoordinates
    ] = useState(null);

    function handlePointerDown(e) {
        e.target.setPointerCapture(e.pointerId);
        setLastCoordinates({
            x: e.clientX,
            y: e.clientY,
        });
    }

    function handlePointerMove(e) {
        if (lastCoordinates) {
            setLastCoordinates({
                x: e.clientX,
                y: e.clientY,
            });
            const dx = e.clientX - lastCoordinates.x;
            const dy = e.clientY - lastCoordinates.y;
            onMove(dx, dy);
        }
    }

    function handlePointerUp(e) {
        setLastCoordinates(null);
    }

    return (
        <div
            onPointerDown={handlePointerDown}
            onPointerMove={handlePointerMove}
            onPointerUp={handlePointerUp}
            style={{
                width: 100,
                height: 100,
                cursor: 'grab',
                backgroundColor: color,
                position: 'absolute',
                border: '1px solid black',
                display: 'flex',
                justifyContent: 'center',
                alignItems: 'center',
                transform: `translate(
          ${position.x}px,
          ${position.y}px
        )`,
            }}
        >{children}</div>
    );
}

export default function Background({
                                       position
                                   }) {
    return (
        <div style={{
            position: 'absolute',
            transform: `translate(
        ${position.x}px,
        ${position.y}px
      )`,
            width: 250,
            height: 250,
            backgroundColor: 'rgba(200, 200, 0, 0.2)',
        }}/>
    );
};


const initialPosition = {
    x: 0,
    y: 0
};


export default function Canvas() {
    const [shape, setShape] = useState({
        color: 'orange',
        position: initialPosition
    });

    function handleMove(dx, dy) {
        setShape({
            ...shape,
            position: {x: dx + shape.position.x, y: dy + shape.position.y}
        })
    }

    function handleColorChange(e) {
        setShape({
            ...shape,
            color: e.target.value
        });
    }

    return (
        <>
            <select
                value={shape.color}
                onChange={handleColorChange}
            >
                <option value="orange">orange</option>
                <option value="lightpink">lightpink</option>
                <option value="aliceblue">aliceblue</option>
            </select>
            <Background
                position={initialPosition}
            />
            <Box
                color={shape.color}
                position={shape.position}
                onMove={handleMove}
            >
                Drag me!
            </Box>
        </>
    );
}

```

#### challenge 3:

```
import { useState } from 'react';
import { useImmer } from 'use-immer';
import Background from './Background.js';
import Box from './Box.js';

const initialPosition = {
  x: 0,
  y: 0
};

export default function Canvas() {
  const [shape, updateShape] = useImmer({
    color: 'orange',
    position: initialPosition
  });

  function handleMove(dx, dy) {
    updateShape(draft => {
      draft.position.x += dx;
      draft.position.y += dy;
    });
  }

  function handleColorChange(e) {
    updateShape(draft => {
      draft.color = e.target.value;
    });
  }

  return (
    <>
      <select
        value={shape.color}
        onChange={handleColorChange}
      >
        <option value="orange">orange</option>
        <option value="lightpink">lightpink</option>
        <option value="aliceblue">aliceblue</option>
      </select>
      <Background
        position={initialPosition}
      />
      <Box
        color={shape.color}
        position={shape.position}
        onMove={handleMove}
      >
        Drag me!
      </Box>
    </>
  );
}

```

### Updating Arrays in State 更新状态数组

#### challenge 1:

```
import {useState} from 'react';

const initialProducts = [{
    id: 0,
    name: 'Baklava',
    count: 1,
}, {
    id: 1,
    name: 'Cheese',
    count: 5,
}, {
    id: 2,
    name: 'Spaghetti',
    count: 2,
}];

export default function ShoppingCart() {
    const [
        products,
        setProducts
    ] = useState(initialProducts)

    function handleIncreaseClick(productId) {
        setProducts(products.map((c) => {
            if (c.id === productId) {
                return {...c, count: c.count + 1};
            } else {
                return c;
            }
        }));
    }

    return (
        <ul>
            {products.map(product => (
                <li key={product.id}>
                    {product.name}
                    {' '}
                    (<b>{product.count}</b>)
                    <button onClick={() => {
                        handleIncreaseClick(product.id);
                    }}>
                        +
                    </button>
                </li>
            ))}
        </ul>
    );
}

```

#### challenge 2:

```
import {useState} from 'react';

const initialProducts = [{
    id: 0,
    name: 'Baklava',
    count: 1,
}, {
    id: 1,
    name: 'Cheese',
    count: 5,
}, {
    id: 2,
    name: 'Spaghetti',
    count: 2,
}];

export default function ShoppingCart() {
    const [
        products,
        setProducts
    ] = useState(initialProducts)

    function handleIncreaseClick(productId) {
        setProducts(products.map(product => {
            if (product.id === productId) {
                return {
                    ...product,
                    count: product.count + 1
                };
            } else {
                return product;
            }
        }))
    }

    function handleDecreaseClick(productId) {
        setProducts(prevState =>  ( prevState.filter(product => {
            return !(product.id === productId && product.count === 1);
        })) )

        setProducts(prevState => (prevState.map(product => {
            if (product.id === productId) {
                return {...product, count: product.count - 1};
            } else {
                return product;
            }
        })) )
    }

    return (
        <ul>
            {products.map(product => (
                <li key={product.id}>
                    {product.name}
                    {' '}
                    (<b>{product.count}</b>)
                    <button onClick={() => {
                        handleIncreaseClick(product.id);
                    }}>
                        +
                    </button>
                    <button onClick={() => {
                        handleDecreaseClick(product.id)
                    }}>
                        –
                    </button>
                </li>
            ))}
        </ul>
    );
}

```

#### challenge 3:

```
import {useState} from 'react';

function AddTodo({onAddTodo}) {
    const [title, setTitle] = useState('');
    return (
        <>
            <input
                placeholder="Add todo"
                value={title}
                onChange={e => setTitle(e.target.value)}
            />
            <button onClick={() => {
                setTitle('');
                onAddTodo(title);
            }}>添加
            </button>
        </>
    )
}

function TaskList({
                      todos,
                      onChangeTodo,
                      onDeleteTodo
                  }) {
    return (
        <ul>
            {todos.map(todo => (
                <li key={todo.id}>
                    <Task
                        todo={todo}
                        onChange={onChangeTodo}
                        onDelete={onDeleteTodo}
                    />
                </li>
            ))}
        </ul>
    );
}

function Task({todo, onChange, onDelete}) {
    const [isEditing, setIsEditing] = useState(false);
    let todoContent;
    if (isEditing) {
        todoContent = (
            <>
                <input
                    value={todo.title}
                    onChange={e => {
                        onChange({
                            ...todo,
                            title: e.target.value
                        });
                    }}/>
                <button onClick={() => setIsEditing(false)}>
                    保存
                </button>
            </>
        );
    } else {
        todoContent = (
            <>
                {todo.title}
                <button onClick={() => setIsEditing(true)}>
                    编辑
                </button>
            </>
        );
    }
    return (
        <label>
            <input
                type="checkbox"
                checked={todo.done}
                onChange={e => {
                    onChange({
                        ...todo,
                        done: e.target.checked
                    });
                }}
            />
            {todoContent}
            <button onClick={() => onDelete(todo.id)}>
                删除
            </button>
        </label>
    );
}

let nextId = 3;
const initialTodos = [
    {id: 0, title: 'Buy milk', done: true},
    {id: 1, title: 'Eat tacos', done: false},
    {id: 2, title: 'Brew tea', done: false},
];

export default function TaskApp() {
    const [todos, setTodos] = useState(
        initialTodos
    );

    function handleAddTodo(title) {
        setTodos([...todos, {
            id: nextId++,
            title: title,
            done: false
        }]);
    }

    function handleChangeTodo(nextTodo) {
        setTodos(todos.map(c => {
            if (c.id === nextTodo.id) {
                return nextTodo;
            } else {
                return c;
            }
        }))
    }

    function handleDeleteTodo(todoId) {
        setTodos(e => e.filter(es => {
            return es.id !== todoId;
        }))
    }

    return (
        <>
            <AddTodo
                onAddTodo={handleAddTodo}
            />
            <TaskList
                todos={todos}
                onChangeTodo={handleChangeTodo}
                onDeleteTodo={handleDeleteTodo}
            />
        </>
    );
}

```

#### challenge 4:

```
import { useState } from 'react';
import { useImmer } from 'use-immer';
import AddTodo from './AddTodo.js';
import TaskList from './TaskList.js';

let nextId = 3;
const initialTodos = [
  { id: 0, title: 'Buy milk', done: true },
  { id: 1, title: 'Eat tacos', done: false },
  { id: 2, title: 'Brew tea', done: false },
];

export default function TaskApp() {
    const [todos, updateTodos] = useImmer(
        initialTodos
    );

    function handleAddTodo(title) {
        updateTodos(draft => {draft.push({
            id: nextId++,
            title: title,
            done: false
        })})
    }

    function handleChangeTodo(nextTodo) {
        updateTodos(draft => {
            const todo = draft.find(t =>
                t.id === nextTodo.id
            );
            todo.title = nextTodo.title;
            todo.done = nextTodo.done;
        })
    }

    function handleDeleteTodo(todoId) {
        updateTodos(draft => {
            const index = draft.findIndex(t =>
                t.id === todoId
            );
            draft.splice(index, 1);
        })
    }

  return (
    <>
      <AddTodo
        onAddTodo={handleAddTodo}
      />
      <TaskList
        todos={todos}
        onChangeTodo={handleChangeTodo}
        onDeleteTodo={handleDeleteTodo}
      />
    </>
  );
}

```

### Reacting to Input with State 通过状态响应输入

#### challenge 1:

```
import { useState } from 'react';

export default function Picture() {
  const [isActive, setIsActive] = useState(false);

  let backgroundClassName = 'background';
  let pictureClassName = 'picture';
  if (isActive) {
    pictureClassName += ' picture--active';
  } else {
    backgroundClassName += ' background--active';
  }

  return (
    <div
      className={backgroundClassName}
      onClick={() => setIsActive(false)}
    >
      <img
        onClick={e => {
          e.stopPropagation();
          setIsActive(true);
        }}
        className={pictureClassName}
        alt="Rainbow houses in Kampung Pelangi, Indonesia"
        src="https://i.imgur.com/5qwVYb1.jpeg"
      />
    </div>
  );
}
```

#### challenge 2:

```
import {useState} from 'react';

export default function EditProfile() {
    const [firstName, setFirstName] = useState("Jane");
    const [lastName, setLastName] = useState("Jacobs");
    const [isSubmit, setIsSubmit] = useState(true);

    let helloWorld = "Hello, " + firstName + " " + lastName + "!";
    let firstNameShow;
    let lastNameShow;
    let buttonShow;
    if (isSubmit) {
        firstNameShow = (<b>{firstName}</b>);
        lastNameShow = (<b>{lastName}</b>)
        buttonShow = "Edit Profile";
    } else {
        firstNameShow = (<input value={firstName} onChange={event => setFirstName(event.target.value)}/>);
        lastNameShow = (<input value={lastName} onChange={event => setLastName(event.target.value)}/>);
        buttonShow = "Save Profile";
    }

    function handleClick(event) {
        event.preventDefault();
        setIsSubmit(!isSubmit);
    }

    return (
        <form>
            <label>
                First name:{' '}
                {firstNameShow}
            </label>
            <label>
                Last name:{' '}
                {lastNameShow}
            </label>
            <button type="submit" onClick={handleClick}>
                {buttonShow}
            </button>
            <p><i>{helloWorld}</i></p>
        </form>
    );
}


```

#### challenge 3:

```
//skip
```



### Choosing the State Structure 选择 State 结构

#### challenge 1:

```
import { useState } from 'react';

export default function Clock(props) {
    const [color, setColor] = useState(props.color);
    return (
        <h1 style={{color:props.color}}>
            {props.time}
        </h1>
    );
}

```

#### challenge 2:

```
import { useState } from 'react';
import AddItem from './AddItem.js';
import PackingList from './PackingList.js';

let nextId = 3;
const initialItems = [
    { id: 0, title: 'Warm socks', packed: true },
    { id: 1, title: 'Travel journal', packed: false },
    { id: 2, title: 'Watercolors', packed: false },
];

export default function TravelPlan() {
    const [items, setItems] = useState(initialItems);
    const [total, setTotal] = useState(3);
    const [packed, setPacked] = useState(1);

    function handleAddItem(title) {
        setTotal(total + 1);
        setItems([
            ...items,
            {
                id: nextId++,
                title: title,
                packed: false
            }
        ]);
    }

    function handleChangeItem(nextItem) {
        if (nextItem.packed) {
            setPacked(packed + 1);
        } else {
            setPacked(packed - 1);
        }
        setItems(items.map(item => {
            if (item.id === nextItem.id) {
                return nextItem;
            } else {
                return item;
            }
        }));
    }

    function handleDeleteItem(itemId) {
        const selectedItem = items.find(item => item.id === itemId)
        if (selectedItem && selectedItem.packed ){
            setPacked(packed - 1);
        }
        setTotal(total - 1);
        setItems(
            items.filter(item => item.id !== itemId)
        );
    }

    return (
        <>
            <AddItem
                onAddItem={handleAddItem}
            />
            <PackingList
                items={items}
                onChangeItem={handleChangeItem}
                onDeleteItem={handleDeleteItem}
            />
            <hr />
            <b>{packed} out of {total} packed!</b>
        </>
    );
}

```

#### challenge 3:

```
import {useState} from 'react';

const initialLetters = [{
    id: 0,
    subject: 'Ready for adventure?',
    isStarred: true,
}, {
    id: 1,
    subject: 'Time to check in!',
    isStarred: false,
}, {
    id: 2,
    subject: 'Festival Begins in Just SEVEN Days!',
    isStarred: false,
}];

function Letter({
                    letter,
                    isHighlighted,
                    onHover,
                    onToggleStar,
                }) {
    return (
        <li
            className={
                isHighlighted ? 'highlighted' : ''
            }
            onFocus={() => {
                onHover(letter.id);
            }}
            onPointerMove={() => {
                onHover(letter.id);
            }}
        >
            <button onClick={() => {
                onToggleStar(letter);
            }}>
                {letter.isStarred ? 'Unstar' : 'Star'}
            </button>
            {letter.subject}
        </li>
    )

}

export default function MailClient() {
    const [letters, setLetters] = useState(initialLetters);
    const [highlightedLetter, sethighlightedLetter] = useState(-1);

    function handleHover(id) {
        sethighlightedLetter(id);
    }

    function handleStar(starred) {
        setLetters(letters.map(letter => {
            if (letter.id === starred.id) {
                return {
                    ...letter,
                    isStarred: !letter.isStarred
                };
            } else {
                return letter;
            }
        }));
    }

    return (
        <>
            <h2>Inbox</h2>
            <ul>
                {letters.map(letter => (
                    <Letter
                        key={letter.id}
                        letter={letter}
                        isHighlighted={
                            letter.id === highlightedLetter
                        }
                        onHover={handleHover}
                        onToggleStar={handleStar}
                    />
                ))}
            </ul>
        </>
    );
}

```

#### challenge 4:

```
import {useState} from 'react';

export const letters = [{
    id: 0,
    subject: 'Ready for adventure?',
    isStarred: true,
}, {
    id: 1,
    subject: 'Time to check in!',
    isStarred: false,
}, {
    id: 2,
    subject: 'Festival Begins in Just SEVEN Days!',
    isStarred: false,
}];

function Letter({
                    letter,
                    onToggle,
                    isSelected,
                }) {
    return (
        <li className={
            isSelected ? 'selected' : ''
        }>
            <label>
                <input
                    type="checkbox"
                    checked={isSelected}
                    onChange={() => {
                        onToggle(letter.id);
                    }}
                />
                {letter.subject}
            </label>
        </li>
    )
}

export default function MailClient() {
    const [selectedIdList, setSelectedIdList] = useState([]);

    // TODO: 支持多选
    const selectedCount = selectedIdList.length;

    function handleToggle(toggledId) {
        // TODO: 支持多选
        setSelectedIdList(prevState => {
            if (prevState.includes(toggledId)) {
                return prevState.filter(value => value != toggledId)
            }else {
                return [...prevState,toggledId];
            }
        })
    }

    return (
        <>
            <h2>Inbox</h2>
            <ul>
                {letters.map(letter => (
                    <Letter
                        key={letter.id}
                        letter={letter}
                        isSelected={
                            // TODO: 支持多选
                            selectedIdList.includes(letter.id)
                        }
                        onToggle={handleToggle}
                    />
                ))}
                <hr/>
                <p>
                    <b>
                        You selected {selectedCount} letters
                    </b>
                </p>
            </ul>
        </>
    );
}
```

### Sharing State Between Components 在组件之间共享状态

#### challenge 1:

```
import {useState} from 'react';

export default function SyncedInputs() {
    const [showInput, setShowInput] = useState("");

    function handleChange(e) {
        setShowInput(e.target.value);
    }

    return (
        <>
            <Input label="第一个输入框" text={showInput} onShow={handleChange}/>
            <Input label="第二个输入框" text={showInput} onShow={handleChange}/>
        </>
    );
}

function Input({label, text, onShow}) {

    return (
        <label>
            {label}
            {' '}
            <input
                value={text}
                onChange={onShow}
            />
        </label>
    );
}
```

#### challenge 2:

```
import {useState} from 'react';

function filterItems(items, query) {
    query = query.toLowerCase();
    return items.filter(item =>
        item.name.split(' ').some(word =>
            word.toLowerCase().startsWith(query)
        )
    );
}

const foods = [{
    id: 0,
    name: '寿司',
    description: '寿司是一道传统的日本菜，是用醋米饭做成的'
}, {
    id: 1,
    name: '木豆',
    description: '制作木豆最常见的方法是在汤中加入洋葱、西红柿和各种香料'
}, {
    id: 2,
    name: '饺子',
    description: '饺子是用未发酵的面团包裹咸的或甜的馅料，然后在沸水中煮制而成的'
}, {
    id: 3,
    name: '烤肉串',
    description: '烤肉串是一种很受欢迎的食物，是用肉串和肉块做成。'
}, {
    id: 4,
    name: '点心',
    description: '点心是广东人的传统喜好，是在餐馆吃早餐和午餐时喜欢吃的一系列小菜'
}];


export default function FilterableList() {
    const [foodsList, setFoodsList] = useState(foods)
    const [query, setQuery] = useState('');

    function handleChange(e) {
        const word = e.target.value;
        setQuery(() => word);
        setFoodsList(() =>
            word === "" ? foods: filterItems(foods,word)
        )
    }

    return (
        <>
            <SearchBar value={query} onChange={handleChange}/>
            <hr/>
            <List items={foodsList}/>
        </>
    );
}

function SearchBar({value: showValue, onChange: showChange}) {

    return (
        <label>
            搜索：{' '}
            <input
                value={showValue}
                onChange={showChange}
            />
        </label>
    );
}

function List({items}) {
    return (
        <table>
            <tbody>
            {items.map(food => (
                <tr key={food.id}>
                    <td>{food.name}</td>
                    <td>{food.description}</td>
                </tr>
            ))}
            </tbody>
        </table>
    );
}

```

### Preserving and Resetting State 保存和重置状态

#### challenge 1:

```
import {useState} from 'react';

export default function App() {
    const [showHint, setShowHint] = useState(false);

    return (
        <div>
            {showHint && (<p><i>提示：你最喜欢的城市？</i></p>)}
            <Form/>
            {
                showHint ? (<button onClick={() => {
                        setShowHint(false);
                    }}>隐藏提示</button> ): (<button onClick={() => {
                        setShowHint(true);
                    }}>显示提示</button>)
            }
        </div>
    );
}

function Form() {
    const [text, setText] = useState('');
    return (
        <textarea
            value={text}
            onChange={e => setText(e.target.value)}
        />
    );
}

```

#### challenge 2:

```
import {useState} from 'react';

export default function App() {
    const [reverse, setReverse] = useState(false);
    const [firstName, setFirstName] = useState("");
    const [lastName, setLastName] = useState("");

    let checkbox = (
        <label>
            <input
                type="checkbox"
                checked={reverse}
                onChange={e => setReverse(e.target.checked)}
            />
            调换顺序
        </label>
    );
    if (reverse) {
        return (
            <>
                <Field label="姓氏" key="lastName" onChange={e => setLastName(e.target.value)} text={lastName}/>
                <Field label="名字" key="firstName" onChange={e => setFirstName(e.target.value)} text={firstName}/>
                {checkbox}
            </>
        );
    } else {
        return (
            <>
                <Field label="名字" key="firstName" onChange={e => setFirstName(e.target.value)} text={firstName}/>
                <Field label="姓氏" key="lastName" onChange={e => setLastName(e.target.value)} text={lastName}/>
                {checkbox}
            </>
        );
    }
}

function Field({label: myLabel, text: showText, onChange: showChange}) {
    return (
        <label>
            {myLabel}：
            <input
                type="text"
                value={showText}
                placeholder={myLabel}
                onChange={showChange}
            />
        </label>
    );
}

```

#### challenge 3:

```
import {useState} from 'react';

function ContactList({
                         contacts,
                         selectedId,
                         onSelect
                     }) {
    return (
        <section>
            <ul>
                {contacts.map(contact =>
                    <li key={contact.id}>
                        <button onClick={() => {
                            onSelect(contact.id);
                        }}>
                            {contact.id === selectedId ?
                                <b>{contact.name}</b> :
                                contact.name
                            }
                        </button>
                    </li>
                )}
            </ul>
        </section>
    );
}

function EditContact({initialData, onSave}) {
    const [name, setName] = useState(initialData.name);
    const [email, setEmail] = useState(initialData.email);
    return (
        <section>
            <label>
                名称：
                <input
                    type="text"
                    value={name}
                    onChange={e => setName(e.target.value)}
                />
            </label>
            <label>
                邮箱：
                <input
                    type="email"
                    value={email}
                    onChange={e => setEmail(e.target.value)}
                />
            </label>
            <button onClick={() => {
                const updatedData = {
                    id: initialData.id,
                    name: name,
                    email: email
                };
                onSave(updatedData);
            }}>
                保存
            </button>
            <button onClick={() => {
                setName(initialData.name);
                setEmail(initialData.email);
            }}>
                重置
            </button>
        </section>
    );
}


export default function ContactManager() {
    const [
        contacts,
        setContacts
    ] = useState(initialContacts);
    const [
        selectedId,
        setSelectedId
    ] = useState(0);
    const selectedContact = contacts.find(c =>
        c.id === selectedId
    );

    function handleSave(updatedData) {
        const nextContacts = contacts.map(c => {
            if (c.id === updatedData.id) {
                return updatedData;
            } else {
                return c;
            }
        });
        setContacts(nextContacts);
    }

    return (
        <div>
            <ContactList
                contacts={contacts}
                selectedId={selectedId}
                onSelect={id => setSelectedId(id)}
            />
            <hr/>
            <EditContact
                initialData={selectedContact}
                onSave={handleSave}
                key={selectedContact?.name}
            />
        </div>
    )
}

const initialContacts = [
    {id: 0, name: 'Taylor', email: 'taylor@mail.com'},
    {id: 1, name: 'Alice', email: 'alice@mail.com'},
    {id: 2, name: 'Bob', email: 'bob@mail.com'}
];

```

#### challenge 4:

```
import { useState } from 'react';

export default function Gallery() {
    const [index, setIndex] = useState(0);
    const hasNext = index < images.length - 1;

    function handleClick() {
        if (hasNext) {
            setIndex(index + 1);
        } else {
            setIndex(0);
        }
    }

    let image = images[index];
    return (
        <>
            <button onClick={handleClick}>
                下一张
            </button>
            <h3>
                {images.length} 张图片中的第 {index + 1} 张
            </h3>
            <img key={image.place} src={image.src} />
            <p>
                {image.place}
            </p>
        </>
    );
}

let images = [{
    place: 'Penang, Malaysia',
    src: 'https://i.imgur.com/FJeJR8M.jpg'
}, {
    place: 'Lisbon, Portugal',
    src: 'https://i.imgur.com/dB2LRbj.jpg'
}, {
    place: 'Bilbao, Spain',
    src: 'https://i.imgur.com/z08o2TS.jpg'
}, {
    place: 'Valparaíso, Chile',
    src: 'https://i.imgur.com/Y3utgTi.jpg'
}, {
    place: 'Schwyz, Switzerland',
    src: 'https://i.imgur.com/JBbMpWY.jpg'
}, {
    place: 'Prague, Czechia',
    src: 'https://i.imgur.com/QwUKKmF.jpg'
}, {
    place: 'Ljubljana, Slovenia',
    src: 'https://i.imgur.com/3aIiwfm.jpg'
}];

```

#### challenge 5:

```
import { useState } from 'react';

function Contact({ contact }) {
    const [expanded, setExpanded] = useState(false);
    return (
        <>
            <p><b>{contact.name}</b></p>
            {expanded &&
                <p><i>{contact.email}</i></p>
            }
            <button onClick={() => {
                setExpanded(!expanded);
            }}>
                {expanded ? '隐藏' : '显示'}邮箱
            </button>
        </>
    );
}

export default function ContactList() {
    const [reverse, setReverse] = useState(false);

    const displayedContacts = [...contacts];
    if (reverse) {
        displayedContacts.reverse();
    }

    return (
        <>
            <label>
                <input
                    type="checkbox"
                    checked={reverse}
                    onChange={e => {
                        setReverse(e.target.checked)
                    }}
                />{' '}
                以相反的顺序显示
            </label>
            <ul>
                {displayedContacts.map((contact, i) =>
                    <li key={contact.name}>
                        <Contact contact={contact} />
                    </li>
                )}
            </ul>
        </>
    );
}

const contacts = [
    { id: 0, name: 'Alice', email: 'alice@mail.com' },
    { id: 1, name: 'Bob', email: 'bob@mail.com' },
    { id: 2, name: 'Taylor', email: 'taylor@mail.com' }
];


```

### Extracting State Logic into a Reducer迁移状态逻辑至 Reducer 中

#### challenge 1:

```

```

#### challenge 2:

```

```

#### challenge 3:

```

```

#### challenge 4:

```

```

