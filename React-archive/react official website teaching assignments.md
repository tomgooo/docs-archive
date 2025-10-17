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