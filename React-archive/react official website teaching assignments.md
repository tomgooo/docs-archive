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

