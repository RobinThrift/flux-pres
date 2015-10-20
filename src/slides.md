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
