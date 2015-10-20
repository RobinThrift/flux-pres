title: What the Flux
author: Robin Thrift
twitter: RobinThrift
homepage: RobinThrift.com
shortcodes: true
css:
    - 'http://fonts.googleapis.com/css?family=Droid+Sans:400,700|Source+Code+Pro|Kaushan+Script'
reveal:
    controls: true
    progress: true
    slideNumber: true
    history: true
    keyboard: true
    overview: true
    transition: 'linear'
    backgroundTransition: 'slide'

-- {
    background: 
        img: '#cb5243'
}

# [var title]

<div class="author-info">
    <h5>[var author]</h5>
    <h5>Jr. Dev, NewStore</h5>
    <a href="http://twitter.com/[var twitter]">@[var twitter]</a>
</div>

--

## What is Flux?

--

### "Application Architecture for Building [emphasize]User Interfaces[/emphasize]"

--

### What is Flux trying to solve?

--

### MVC

![img/mvc1.svg](img/mvc1.svg)

--

### MVC

![img/mvc2.svg](img/mvc2.svg)

-- {
    transition: 'slide-in none-out'
}

![img/mvc3-1.svg](img/mvc3-1.svg)

-- {
    transition: 'none-in slide-out'
}

![img/mvc3-2.svg](img/mvc3-2.svg)


-- {
    transition: 'slide-in none-out'
}

![img/chat-0.svg](img/chat-0.svg)

-- {
    transition: fade
}

![img/chat-1.svg](img/chat-1.svg)

-- {
    transition: 'none-in slide-out'
}

![img/chat-2.svg](img/chat-2.svg)

--

![img/flux_overview.svg](img/flux_overview.svg)

--

## [colour hex=489541]The Dispatcher[/colour]
![img/dispatcher-0.svg](img/dispatcher-0.svg)

--

```typescript
interface Dispatcher {
    register(fn: (payload: Payload) => void): void;
    dispatch(payload: Payload): void;
}
```

```typescript
type Payload = {
    actionType: Symbol,
    data: any
}
```

-- {
    transition: 'slide-in none-out'
}

![img/dispatcher-1.svg](img/dispatcher-1.svg)

-- {
    transition: 'none-in slide-out'
}

![img/dispatcher-2.svg](img/dispatcher-2.svg)

-- 

## [colour hex=74299F]Stores[/colour]
![img/stores-0.svg](img/stores-0.svg)

-- {
    transition: 'slide-in none-out'
}

```typescript
interface Store {
    dispatch(payload: Payload): void;
}
```

-- {
    transition: 'none-in slide-out'
}

```typescript
interface Store<T> {
    public dispatch(payload: Payload): void;
    public registerView(fn: (oldState: T, newState: T) => void): void;
    private notifyViews(): void;
}
```

--

```typescript
class UserStore extends Store<User[]> {
    // ...
    dispatch(payload: Payload) {
        switch (payload.actionType) {
            case 'ADD_USER':
                // ...
            break;
            case: 'UPDATE_USER':
                // ...
            break;
        }
    }
    // ...
}
```

[fragment]
```typescript
import dispatcher from './localDispatcher';
let userStore = new UserStore();
dispatcher.register(userStore.dispatch);
```
[/fragment]

-- {
    transition: 'slide-in none-out'
}

"[...] stores accept updates and reconcile them as appropriate [...]"

[fragment]
"[...] Stores have no direct setter methods [...], but instead have only a single way of getting new data into their self-contained world."
[/fragment]

<hr />

[small][https://facebook.github.io/flux/docs/overview.html](https://facebook.github.io/flux/docs/overview.html)[/small]

-- {
    transition: 'none-in slide-out'
}

"[...] stores accept updates and reconcile them as appropriate [...]"

"[...] Stores have no direct setter methods [...], but instead have only a single way of getting new data into their [emphasize]self-contained world[/emphasize]."

<hr />

[small][https://facebook.github.io/flux/docs/overview.html](https://facebook.github.io/flux/docs/overview.html)[/small]

--

## [colour hex=4A4A4A]Views[/colour]
![img/views-0.svg](img/views-0.svg)

--

```javascript
class AutoComplete extends React.Component {
    _handleChange(event) {
        let {value} = event.target;
        this.setState({value});
        autoCompleteActions.createListForValue(value);
    }
    onStoreUpdate(oldState, newState) {
        this.setState({suggestions: newState});
    }
    render() {
        // next slide
    }
}
```

--

<pre><code class="lang-typescript">render() {
    <span class="hljs-keyword">return</span> (
        &lt;input <span class="hljs-keyword">type</span>=<span class="hljs-string">"text"</span> 
               value={<span class="hljs-keyword">this</span>.state.value} 
               onChange={<span class="hljs-keyword">this</span>._handleChange.bind(<span class="hljs-keyword">this</span>)} /&gt;
        &lt;ul&gt;  
            {<span class="hljs-keyword">this</span>.state.suggestions.map((s) =&gt; {
                <span class="hljs-keyword">return</span> <span class="xml"><span class="hljs-tag">&lt;<span class="hljs-title">li</span>&gt;</span>{s}<span class="hljs-tag">&lt;/<span class="hljs-title">li</span>&gt;</span>;</span>
            })}
        &lt;/ul&gt;  
    );
}
</code></pre>
