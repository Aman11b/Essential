
 ## COMPONENTS
 * building block of UI
 * react renders the view of each component
 * component has its own data login and appearance
 * componenets can be reused nested inside and pass data between them



 ## component as function
 * 1->component name start with capital letter
 * 2->function needs to return some markup jsx or null
 * 3->each component returns exactly one element
 * 4->never nest component declaration


 ## JSX
 * -> declerative syntax to describe what component look like and how they work
 * -> each component retrun one block of JSX
 * -> extention of JS embed HTML + CSS and react
 * -> babel convert JSX(browser dont understand it) to JS
 * -> imperative approach (JS manually tell all to do)
 * -> declarative appraoch(just describe what ui should look like)


 ## React fragment
 * lets you add element without leaving trace in HTML tree so in DOM
 * just add <></> or <React.Fragment> thats it
 * sometimes key is required while rendering list
 * it allow more then one element inside JSX

 ## PROPS (PROPERTY)
 * ->passing data between components from parent to child components
 * ->first pass prop in component then receive it then
 * -> pass info down the tree
 * -> can pass any value in prop
 * -> props are ready-only => data in component is made from props (data coming from parent component basically outside)and state(internal component data that can be updated by logic basically inside)
 * -> props cant be modified by child component that are read only to mutate prop you need state
 * -> prop is obj if u change you change parent too and that cause side effect coz u are changing data which is outside ,react is pure function that means not affecting outside
 * -> one way data flow=> only from parent to child not opposite only top to bottom (not in angular) it makes application predictable and easier, debug becomes easy, two way data binding is less efficent

 ## RULES OF JSX
 * -> essestially HTML but with {can add JS code}
 * -> {statement are not allowed here like if else or for or switch}
 * -> JSX -> JS expression
 * -> a peace of JSX has on root element

 ## PROPS
 * -> props always exists in all components
 

 > StrictMode-> render twice in order to find bugs and check if outdated parts of API

 
 ## STATE
 * -> data a component can hold over time, ifo that component needs to remember though its life cycle
 * -> its kindoff memory that can be changed
 * -> state variable/peice of state a single variable in a component
 * -> state is an entrire condition at ant point of time > all peices ofm state together
 * -> updating state re-render component (one single component render its called a view all views together makes final UI)
 * -> with state react keep UI sync with data
 * ->useState retusn a array it takes defaut value and a function
 * -> useState is called hooks(but only in top level of function not in if or loop or something else)
 * ->dont update state manually
 * -> always term state as im-mutable and use setter function for updates

 ## mechanics of state
 * -> we dont manipulate state directly then how to update
 * -> react upadate conmpoenent view by completely rerending the component
 * -> react maintains a state which remain contant through the rerendering unless the component is removed from UI which is called un-mounting


 ## State vs Prop
 * -> state is internal data owned by component,component memory,can be updated by component itself,updating leads to rerendering ,used to make component interactive
 * -> props is external data owned by parent,read-only,when new prop is received re-rendering happens,used by parent to configure child component
 */


 ## THINKING IN REACT
 * -> break the desired UI into components and establish the component tree
 * -> build a static version
 * [state management]
 * -> think about state
 * - when to use state
 * - type os state logical or global
 * - where to place state
 * -> establish the data flow
 * - one way data flow
 * - parent to child communication
 * - accessing global state

 ## FUNDAMENTALE OF STATE MANAGEMENT
 * -> deciding when to create a peice of state what type of state are necessary where to place each peices of state and how data flows through the app
 * ->LOCAl STATE
 * - state needed only by one or few component
 * - alway start with local state
 * -> GLOBAL STATE (shared stae)
 * - state that many component might need
 * - implemented by content api or redux
 * -> WHEN and WHERE
 * -> need to store data( will this data change ? yes : regular variable) is can be computed then use previous existing state derived state > should it re-render component > no then REF (useRef, no re-render) > yes now create new state
 * -> WHERE
 * -> is needed in one component then leave it there
 * -> if can be needed in chalid component then pass it as props
 * -> if used by one or few sibling component -> left state to first commen parent (lifting state up)
 * -> if need in more sibilings then its global state


 ## LIFTING UP STATE
 * -> problem sharing state with sibliing component
 * -> lift it to closest common parent component
 * [data can only flow down to childen via props not sideways to siblings]
 * -> how a child promotion(child) update sate in checkout(parent) > pass setCoupon down to component which need to update the state


 ## DERIVED STATE
 * -> state that is computed from an existing peice of state or from props

## CHILDREN PROP
* -> an empty "hole" thta can be filled by any JSX the component receive as children
* -> insted of <button/> write more JSX <button>{here}</button> like html
* -> children of button,accessible through prop.children
* -> children prop allows us to pass JSX into a element
* -> essential tool to make resuable and configure component

## Prop Drilling
* -> whenever we are passing prop just so that it can reach to some other component and this one act as intermediate with no use of that prop

 ## HOW TO SPLIT UI IN COMPONENTS
 * -> Huge component
  - too many responsibility
  - might need too many props
  - hard to reuse
  - complex code,hard to undersatnd
 
  -> Small component
  - we will end up with 100s of mini components
  - confusing codebase
  - too abstracted
 
 * ->how to split
  - logical seperation
  - some are reusable
  - low complexity
 
 * -> 4 critrtia
  1. logical seperated of content/layout
     - does the conmponent contain peices of content or layout that dont't belong together?
     - is it possible to reuse part of this component?
     - do you want/need to reuse it?
     - is the component doing too many different things?
     - does the component reply on too many props?
     - does the component have too many peice of state and/or effect?
     - is the ocde ,including JSX ,too complex/confusing?
     - do you prefer smaller function/components?
     ### - If yes then you need a new component
 
  2. reusability
  3. responsibilities/complexity
  4. personal coding style
 
 ## GENERAL GUIDELINES
 * -> creating new component creates a new abstraction
 * -> name the component according to what it does or what it displays
 * -> never declare a new component inside another component
 * -> co-locate related components inside same file

## Component categories
 * -> stateless/presentational component
 * - no state
 * -receive prop and simpley present received data or other content
 * - usually small and reusable
 * -> stateful component
 * - have state
 * - can be reusable
 * -> structural component
 * - Pages, Layouts Screen or app
 * - esult of composition
 * - can be huge and non-reusable
 * - provide structure
  
 ## COMPONENT COMPOSITION
 * -> using a component inside a compoent dont let it to be reused
 * -> in component composition we pass children as a prop and now the component is reusable too
 * -> component composition is combining different compoent using the children prop (or explicitly defined props)
 * ->WE use component composition in 2 cases
 * - create highly reusable and flexible components
 * - fix a prop drilling (great for layouts)
 * - possible because components dont need to know their children in advance

  ## COMPONENTS,INSTANCES,ELEMENTS
 * -> Components
 * - describe the UI
 * - component is a finction that retusn React element(element tree) ,usually written as JSX
 * - blueprint or template (using this component instances are created)
 * -> Instances
 * - instances are created when we use component
 * - instance is actual physical manifestation
 * - has its own state and prop
 * - has a lifecycle(can be born live and die)
 * -> Element
 * - as instances are executed react return a element
 * - JSX is converted to React.createElement() function call -> resulting react element
 * - it has all necessary info to create DOM element
 * COMPONENT (<Tab />) -> Component instances ( Returns) -> React Element (Inserted to DOM) -> DOM Element (HTML)

 ## $$typeof: Symbol(react.element)
 * -> this protects from cross site scripting attacts
 * -> Symbol are javaScript primitive which cant be trasnmitted via json
 * -> a symbol like this cant come from API call
   
```
console.log( <DifferentContent test={23} /> );
```
> this is type DifferentContent

```
console.log(DifferentContent());
```
> this is type div -> raw react element not component instances

## How rendering works > Overview
 * -> Reacp
 * - component -> component instances -> react element -> DOM Element -> UI
 * -> how react element change into DOM element
 * => How component are displayed on the screen
 * -> Render is triggered (by updating state somewhere) => Render Phase(react calls component finction and figure out how DOM should be updated) => Commit phase (React actaully writes to the DOM ,updating ,inserting nad deleting element) => Browser paint
 * -> in react ,rendering is NOT updating the DOM or displaying element on the screen.
 * -> Rendering only happens internally inside React,it does not produce visual changes

## How render are trigged
 * 1. Initial render of the application(when it runs for very first time)
 * 2. State is updated in one or more component instances(re-render)
 * -> render process is triggered for entire application
 * -> render are not triggred immediately, but scheduled for a when the JS engine has some " free time" (few miliseconds ).There is also batching of multiple setState calls in event handlers

## Review: Mechanics of state in react
* -> Not true #1: Rendering is updating the screen/dom (its calling component function )
* -> Not true #2: React completely discard old view(DOM) on re-render

 ## RENDER PHASE
 * 1. component instances that trigger re-render 
 * 2. react element
 * 3. new virtual DOM 
  - => VIRTUAL DOM (React element tree)
  - -> component tree -> react element tree(virtual DOM)
  - -> Virtual DOM: Tree of all react element created from all instances in the component tree
  - -> Cheap and fast to create multiple trees
  - -> nothing to do with Shadow DOM(brpwser technology used in web component)
  - -> in rerender new component tree is created and a new react element tree is creted
   ### Rendering a component will cause all of the child component to be rendered as well(no matter if porp changed or not) -> necessary because react doesn;t know weather children will be affected -> virtual DOM created again
* 4. Reconciliation + Diffing (Current fiber tree > before state update) 
  - its is done in react reconciler (Called Fiber)
  => WHat is reconsiliation and why do we need it?
  - creating react element tree is cheap and fast coz its just object but writing DOM is not is is relatively slow
  - usually only a small of DOM needs to be updated
  - react reuses as much of the exixtsing DOM as possible
  => how to know which DOM is changed -> reconciliation
  ### Reconciliation: Deciding which DOM elements actually need to be inserted ,deleted,or updated in order to reflect the latest state changes done by a reconciler(real engine of react current > reconciler is Fiber)
  => The Reconciler : Fiber
  - takes entire react element tree(virtual tree) -> (on initial render) -> creates Fiber tree
  ### Fiber Tree: internal tree that has a "fiber" for each component instance and DOM element
  - Fibers are not re-created on every render (its never destroyed just get mutated again and again over future reconciliation)
  (Fiber{"Unit of work"} -> (current state,Props,Side effects,Used Hooks,Queue of work,...))
  - each fiber is linked to it parent,all other has link to there previous sibling (linked list)
  - Virtual and Fiber tree has componet with DOM element too ,they are complete representaion of DOM structure
  - Work can be done asynchronously (Rendering process can be split into chunks,tasks can be prioritized,and work can be paused,reused or thrown away)
  -- enables conurrent feater like suspense or transitions starting react18
  --long render wont block JS engine
  => Reconciliation in Action
  - is there a a state update -> new virtual DOM is created-> new dom is reconcided + Diffing (Comparing elemtn based on there position in the tree is called diffing) with current fiber tree-> updated fiber tree(workInProgress tree) 
* 5. Updated Fiber tree
* 6. List of DOM updates => Result of the render phase ("list of effects"


  ## THE COMMIT PHASE AND BROWSER PAINT
 * 1. List of DOM update -> Update DOM
 * - React writes to the DOM: inserting ,deleting, and updates (list of DOM updates are "flushed" to the DOM)
 * - Committing is synchronous: DOM is updated in one go,it can't be interrupted.This is necessary so thta the DOM never shows partial result,ensuring a consistent UI(in sync with all times)
 * - after the commit phase is completes,the workInProgress fiber tree becomes the current tree for the next render cycle
 * (BROWSER PAINT)
 * 2. Updated UI on the screen
  > render phase (react) -> commit phase (ReactDOM) -> browser paint(browser)
  - react does not touch the DOM.react only renders.it doesnt know where the render result will go
  - react can be used on different platforms (Reactive Native -> iOS android, Remotion -> video, many more...)
 

## RECAP
 * 1. trigger(happen only on initila render or state update)
 * 2. render phase () -> updated react element-> new virtual DOM-> reconcilied and diffing with current fiber tree-> updated fiber tree -> list of DOM update
 * - do not pruduce any visual output
 * - rendering a component also renders all of its child component
 * - render is asynchronous: work can be split,prioritised ,paused and resumed
 * 3. Commit phase
 * - Updated DOM
 * - Synchronous : DOM update are written in on go ,to keep UI consistent
 * 4.Browser Paint (updated UI on screen)

## How Diffing works
 * -> 2 Fundamental Assumption
 * - Two element of different types will produce different trees
 * - Element with a stable key prop stay the same across renders
 * => this allowes reqact to go from O(n^3) to O(n) operations per 1000 element
 * -> its comparing element by element based on its position in tree
 * 1. Same position,different elelemt
 * - React assume entire sub-tree is no longer valid
 * - old component are destroyed and removed from DOM ,including state
 * - tree might be rebuilt if children stayed the same(state is reset)
 * 2. Same position ,same element
 * - element will be kept (as well as child element), including state
 * - sometimes this is not what we want.. then we can use key prop

  ## KEY PROP
 * -> special prop that we use to tell the diffing algo that an element is unique
 * -> allow react to distinguish between multiple instances of the same component type
 * -> when a key stays the same across renders,the elelemt will be kept in DOM(even if the position in the tree changes)
 * - using key in list
 * -> when a key chnages between render,the elelemt will be destroyed and a new one will be created (even if the position in the tree is the same as before)
 * - using key to reset the state
 * 1. KEYS IN LISTS (STABLE KEY)
 * -> no key-> adding a new list item -> same element ,but different position in tree,so they are removed and recreated in the DOM(bad for performance)
 * -> with keys -> adding new lits item ->different position in the tree but the key stays the same,so the element will be kept in DOM
 * 2. KEY PROP TO RESET STATE (CHANGING KEY)
 * -> if we have the same element at the same position in the tree the dom elelemt  and state will be kept
 * -> if we have a question component with a answer and we chnage the question the answer will remain the same and irrelevent in this case coz of the rule hnece use key so that its is differentiated and the sate will be reset

 ## TWO TYPES OF LOGIC IN REACT COMPONENT
 * 1.render logic
 * -> code that lives at the top level of th component function
 * -> participate in describing how the component view looks like
 * -> executed every time the component renders
 * 2.event handeling function
 * -> exexcuted as concequences of the event that the handler is listening for
 * -> code that actually does things
 
 ## FUNCTIONAL PROGRAMMING PRINCIPLES
 * 1.Side effect: dependency on or modification of any dat outside the function scope."Interration with outside world".Example: mutating external variable,HTTP request,Writing to DOM
 * 2.Pure function:a function that has no side effects
 * -> given the same input ,a pure function will always return the same output

 ## RULES FOR RENDER LOGIC
 * -> component must be pure when it comes to render login: given the same prop(input), a component instances should always return the same JSX (output)
 * -> render login must produce no sde effects: no interaction with the "outside world" is allwed.
 * So, in rende logic:
 * - Do not perform network request (API Calls)
 * - Do not start timer
 * - Do not directly use the DOM API
 * - Do not mutate object or variable outside of the function scope(This is why we cant mutate props)
 * - Do not uodate state(or Ref): this will create an infinite loop


 ## STATE UPDATE BATCHING
 * => How state update are batched
 * -> Render are not triggered immediately,but scheduled for when JS engine has some "free time".There is also bacthing of multiple setState call in event handlers
```
  const reset=fuction(){
   setAnswer("")
   console.log(answer)
   setBest(true)
   setSolved(false)
}
 ```
* -> it does not update state and render+ commit 3 times 
* -> all will be batched as one state update for entire event handler then redner+commit(just one render and commit per event handler)
* -> but what will be value of console.log 
* -> statee is stored in fiber tree during render phase 
* -> at this point,re-render has not happened yet
* -> therefore ,answer still containes current state,not the updated state(" ") -its is "Stale state"
* => that is why upadting state in react is asynchronous
* -> updated state variable are not immediately available after setState call,but only after the re-render
* -> this is also applies when only one state variable is updated
* -> if we need to update state based on previous update,we  use setState with call back(SetAnswer(answer=> ...))
* => Batching beyond event handler function
* -> automatic bathcing for event handler was in react 17 its for timeout and promises and native events too in react18+ 


 ## LIBRARY vs FRAMEWORK vs THE REACT ECOSYSTEM
 * -> Framework (all in one kit)
 * - everything you need to build a completed application is included in the framework("batteries included")
 * -> liberary (seperate ingredient)
 * - view library (react just draw component on UI)
 * - enternal library is needed
 

## Practical summary
 * -> a component is like a blueprint for a piece of UI that will eventually exist on the screen.When we "use" a component ,React create a component instance,which is like an actual physical manifestation of a component,containing prop,state na dmore. A component instance,when rendered,will return a React Element
 * -> Rendering only menas calling component function and calculating what DOM element need to be inserted deleted and updated.It has nothing to do with writing to DOM.Therefore each time a component instance is rendered and re-rendered the function is called again
 * -> only the initail app render and state update can cause a render,which happens for the entire application ,not just one single component
 * -> when a component instance gets re-rendered,all its children will get re-rendered as well.This doesnt mean that all children will get updated in the DOM,thanks to reconciliation ,whic checks which element hasve actually changed between two render.But all this re-rendereing can still have an impact on performance
 * -> diffing is how react decide which DOM element needs to be added or modified.If between render a certain react element stays at the same position in the element tree the corresponding DOM element and compoent state will saty the same.If the element changed to a different position of if it's a different element type the DOM element and state will be destroyed
 * -> giving element a key prop allow react to distinguish between multiple component instances.When a key stays the same across render,the element is kept in the DOM.This is why we need to use keys in list.When we chnage the key between reander the DOM element will be destroyed and rebuilt we use this as trick to reset state
 * -> never declare a new component inside another component,Doing so will re-create the nested component everytime the parent component re-render REqact will always see the nested component as new,and there reset its state each time the parent state is updated
 * -> the logic that produce JSX output for a component instances("render" logic) is not allowed to produce any side effect: no API calls no timer no object or variable mutation no state update. Side effect are allowed in event handler and userEffect
 * -> The DOM is udpated in the commit phase,but not by react but by a "renderer" called REACTDOM.Thats's why we always need to include both liberary in a react web app project. We can use other renderer to use react on different platforms for ep to built mobile or native apps
 * -> multiple state update inside an event handler function are batched so they happen all at once causing only one re-render.This means we can not access a state variable immediately after undating it: state udpate are asynchronous.Since react 18 batching also happens in timeout promises native and handlers
 * -> using event in event handlers we get access to a synthetic event object not the browser native object so that event work the same way across all browser.The difference is that most synthetic event bubble, including focus blur and chnage which do not bubble as native browser event. only the scroll vent does not bubble
 * -> react is a libery not a framework.This means that you can assemble your application using your favorite 3rd party liberary.The downside is that you need to find and learn all these additional liberies

## Component(instance) lifecycle
 * 1. Mounted/Initial render
 * - component instance is rendered for the first time
 * - fresh state and prop are created
 * 2. re-rendered(unlimited times)
 * - state change
 * - prop change
 * - parent change
 * - context change
 * 3. unmounted
 * - component instance is destoyed and removed
 * - state and prop are destroyed


## A First look at effect
 * -> Side effect is basically any interaction between a react component and the world outside the compnent
 * -> side effect should not happend in render logic
 * -> side effect can be implement by event handlers(function triggered) and effect(useEffect) - Effect allow us to write code that will run at different moment:Mount re-ender or un-mount



## Event handler
 * - executed when the corresponding event happens
 * - use to react to an event
 * - preferred way to create side effects
 * Effect
 * - executed after the component mount(initial mount) and after subsequent re-render(accourding to dependency array)
 * - each one has Effect code + Cleanup function + dependency array
 * - used to keep a component synchronized with some external system

## * DEPENDENCY ARRAY
 * -> BY default effect run after every render we can prevent that by passing a dependency array
 * -> without the dependency array ,React doent know when to run the effect
 * -> Each time one of the depnedecies change the effect will be executed again
 * ### every state variable and prop used inside the effect MUST be included in the dependency array (otherwise we get a "stale closure")
 * => useEffect is like an event listener that is listeniing for one dependency to change,Whenever a dependency chnages it will execute the effect again
 * -> effect react to update to state and props used inside the effect(the dependency).So effect are "reactive"
 * -> Component state/prop -> synchronize with -> external system(side effect)
 => Dependency(state or prop chnages)-> effect is executed again,component is re-rendered (effect and component lifecycle are deeply connected)
 -> we can use the dependency array to run effect ehrn the component render or re-renders

 | Hook Usage | Synchronization | Lifecycle |
|-------------|----------------|-----------|
| `useEffect(fn)` | Syncs with every render | Runs after every render |
| `useEffect(fn, [])` | No dependencies | Runs only once after mount |
| `useEffect(fn, [x])` | Syncs with `x` | Runs on mount and when `x` changes |
| `useEffect(fn, [x, y, z])` | Syncs with `x`, `y`, `z` | Runs on mount and when any dependency changes |

* => when are effect executed (timeline)

### Mounting(initial render)-> commit -> browser paint -> EFFECTS(if effect sets state ,an additional render will be required thast why it happens later) -> (title change -> re-render -> commit ->LAYOUT EFFECT -> browser paint -> CLEANUP -> EFFECT) -> unmount -> CLEANUP

 ## THE CLEANUP FUNCTION
 * -> function that we can return from an effect(optional)
 * -> Runs on two occation
 * - 1. before the effect is executed
 * - 2. after a component has unmounted
 * -> component render=> execute effect if dependency array includes updated data
 * -> component unmount-> execute cleanup function
 * -> necessary whenever the side effect keeps happening after the component has been re-rendered or unmounted
 * -> eg: http request > cancel request in cleanup,API subscription > cancel subscription,start timer > stop timer,add event listener > remove listener
 * -> each effect should do only one thing! use on useEffect hook for each side effect.This makes effect easier to clean up

```
  useEffect(
    function () {
      if (!title) return;
      document.title = `Movie | ${title}`;

      return function () {
        document.title = "popCorn";
        console.log(`Clean up effect for movie ${title}`);
      };
    },
    [title],
  );
```
> clean up function triggers on unmount still this will console the title ,how is it saving the title after getting unmounted the reason is closure,closure in JS mean a function will always remeber all the variables that were present at the time and place data function was created,when the cleanup was created title was alreadt set to a certain value thast why it remembers it

## cleanup for data fetching

```
 useEffect(
    function () {
      const controller = new AbortController();
      async function fetchMovies() {
        try {
          SetIsLoading(true);
          setError("");
          const res = await fetch(
            `http://www.omdbapi.com/?apikey=${KEY}&s=${query}`,
            { signal: controller.signal },
          );

          if (!res.ok) throw new Error("Some went wrong with fetching movie");

          // this is side effect
          const data = await res.json();
          if (data.Response === "False") throw new Error("❌ Movie not found");
          setMovies(data.Search);
          setError("");
        } catch (err) {
          // console.error(err.message);
          if (err.name !== "AbortError") {
            setError(err.message);
          }
        } finally {
          SetIsLoading(false);
        }
      }
      if (query.length < 3) {
        setMovies([]);
        setError("");
        return;
      }
      fetchMovies();

      return function () {
        controller.abort();
      };
    },
    [query],
  );
```
> on every keystoke component gets re-render and then the clean up will be called as it triggers between re-render too,so each time a re-render happens the controller will abort the current fetch request, that is eactly what we want to cancel request

> one problem with this is as soon as it get cancelled JS sees it as an error,but we can ignore it with this
```
          if (err.name !== "AbortError") {
            setError(err.message);
          }
```
 ## WHAT ARE REACT HOOKS?
 * -> special built-in function that allows us to "hook" into react interations:
 * - creating and accessing state from fiber tree
 * - registering side effects in fiber tree
 * - manula DOM selection
 * -> always start with "use"
 * -> enables easy reusing of non-visula logic:we can compose multiple hooks into out own custom hooks
 * -> give function component the ability to won state and run side effect at different lifecycle point(before v16.8 only available in class component)

 ## OVERVIEW OF ALL BUILT-IN HOOKS
 | Most used   | Less used            | Only for libraries       |
|-------------|----------------------|--------------------------|
| useState    | useCallback          |                          |
| useEffect   | useMemo              |                          |
| useReducer  | useTransition        |                          |
| useContext  | useDeferredValue     | useSyncExternalStore     |
|             | useLayoutEffect      | useInsertionEffect       |
|             | useRef               |                          |
|             | useId                |                          |
|             | useImperativeHandle  |                          |
|             | useDebugValue        |                          |

 ## THE RULES OF HOOKS
 * 1.  only call hooks at the top level
 * - do not call hoooks inside conditionals,loops,nested function, or after an early return
 * - this is necessary to ensure that hooks are always called in the same order(hook rely on this)
### HOOKS REPLY ON CALL ORDER
 * -> react element tree(virtual DOM) - (on initial render) Fiber tree -> Fiber(props,..,linkedlist of hooks)
 * > is you called hook in conditions and suppose there are many hooks formed in form of linked list and if suppose one condition retuned false that means that hook is vanished but now what will happen to the link list now we have a hole in link list which is not possible
 * > why linked list then ,coz it a simplest way to represent to assocaite each hook with its value
 * 2.  only call hooks from react function
 * - only call hooks inside a function component or a custom hook
 * > these rules are automatically enforced by React's ESLint rules

 ## Summary of defining and updating sytate
  -> what ever we pass in useState is in initial state,react will only look at it on initial state that is when it mounts
 1. creating state
  - Simple
  ```
   const [count,setCount]=useState(23);
  ```
  - based on function(lazy evaluation)
```
   const [count,setCount]=useState(()=>localStorage.getItem("count"));
 ```
  > function must be pure and accept no argument,called only on initial render
 2. Updating state
  - Simple
  ```
   setCount(1000);
  ```
  - Based on current state
  ```
   setCount((c)=>c+1)
  ```
  > Function must be pure and return next state
  ### make sure to NOT mutate object or array,but to replace them

## WHAT ARE REFS?
 * -> "BOX" (object) with a mutable .current property that is persistsed across renders("normal veriable are always reset")
 * -> we can write to and read from the ref using .current
 * -> Two big use cases
 * - creating a variable that stays the same between renders(eg previous stsate,setTimeout id etc..)
 * - selecting and storing DOM element
 * -> Refs are for data that is not rendered:usually only appear in event handlers or effect,not in JSX (otherwise use State)
 * -> Do not read or write .current in render logic(like state)
   
 | Feature / Behavior                              | State | Ref |
|-------------------------------------------------|:----:|:---:|
| Persistent across re-renders                    | ✅   | ✅  |
| Updating it causes component re-render          | ✅   | ❌  |
| Value is immutable (should not mutate directly) | ✅   | ❌  |
| Updates are asynchronous                        | ✅   | ❌  |

 ## RESUSING LOGIC WITH CUSTOM HOOKS
 * -> we can reuse two things in react a piece of UI(component) or logic(does logic have any hooks-(yes)-> Custom Hook -(No)-> Regualr function)
 * -> allow us to reuse non-visual logic in multiple components
 * -> one custom hook should have one purpose,to make it reusable and portable(even across multiple projects)
 * -> rules of hooks apply to custom hooks too
 * -> basically its just a JS function,unlike component it can receive and return any relevent data(usually [] or{})
 * -> custom hooks need to use one or more react hooks
 * -> fucntion names needs to start with use
 * => when to create one
 * - we want to reuse some part of non-visual logic
 * - simpley want to extract a hig part of our component out into some custom hook

## Class Component vs Function Component (React)

| Feature / Category | Function Component | Class Component |
|--------------------|-------------------|-----------------|
| Introduction Version | Introduced with Hooks in React v16.8 (2019) | Introduced earlier around React v0.13 (2015) |
| Existence | Existed since early React but without Hooks | Core way to create components before Hooks |
| How to Create | JavaScript function (arrow function or normal function) | ES6 class extending `React.Component` |
| Reading Props | Destructuring or `props.x` | `this.props.x` |
| Local State | `useState` Hook | `this.state` and `this.setState()` |
| Side Effects / Lifecycle | `useEffect` Hook | Lifecycle methods (`componentDidMount`, `componentDidUpdate`, `componentWillUnmount`) |
| Event Handlers | Regular functions inside component | Class methods |
| Returning JSX | Return JSX directly from function | Return JSX from the `render()` method |

---

## Advantages of Function Components

| Advantage | Explanation |
|-----------|-------------|
| Easier to build | Less boilerplate compared to classes |
| Cleaner code | Hooks make code shorter and easier to read |
| Unified side-effect handling | `useEffect` combines multiple lifecycle behaviors |
| Easier state logic sharing | Custom Hooks allow reusable stateful logic |
| No `this` keyword | Avoids confusion with `this` binding |
| Modern React standard | Recommended approach in modern React apps |

---

## Advantages of Class Components

| Advantage | Explanation |
|-----------|-------------|
| Explicit lifecycle methods | Lifecycle phases are clearly separated |
| Familiar OOP style | Developers comfortable with classes may find it intuitive |
| Still supported | Older projects and legacy codebases use class components |

>  hooks works in function component not in class components

>  in class we have one huge state object now multiple state variables


## useReducer hook
 * -> more advance and complex way to manager state
 * - useReducer hook works wth reducer function(pure function),that takes previous state so-called action as an argument and then return the next state
 


 ## why userReducer
 * -> state management with useState is not enough in certain situations:
 * - when component have lot of state variables and state updates,spread across many event handlers all over the component
 * - multiple state update need to happen at the same time (as a reaction to same event like starting a game)
 * - updating one peice of state depends on one or multiple other peices of state
 

## Managing state with useReducer
 * -> an alternative way of setting state,ideal for complex state and related peice of state
  ```
  const [state,dispatch]=useReducer(reducer,initialState);
  ```
 * - store related piece of state in a state object
 * - userReducer needs reducer:function containing all logic to update state,Decouples state logic from component
 * - reducer: pure function(no side effects) that takes current state and actionb,and return the next state
  ```
  function reducer(curState, action) {
  switch (action.type) {
    case "dec":
      return { ...curState, count: curState.count - curState.step };
    case "inc":
      return { ...curState, count: curState.count + curState.step };
    case "setCount":
      return { ...curState, count: action.payload };
    case "setStep":
      return { ...curState, step: action.payload };
    case "reset":
      return initialState;
    default:
      throw new Error("unknown action");
  }
}
  ```
- action:object that describe how to update state(has action type and payload)
- dispatch:function to trigger state updates,by "sending"action from event handlers to the reducer(similar to setState)
 


 ## how reducer update state
 * -> updating state in a component-> dispatch(action -type:"updateDay" payload=23)->reducer(tate action and current state and return)-> next state-> re-render
 > reducer is called reducer coz its just like arr.reduce(),reduces acuumulate("reduce") action over time

## ROUTING
 * -> with routing,we mathc differetn URLs to differetn UI views(React Component):routes
 * -> this enables user to navigate between different application screens using the browser URL
 * -> keep the UI in sync with current browser URL
 * -> routing is delt by 3rd party package react router
 * -> allows us to built single page application



 ## SINGLE PAGE APPLICATION
 * -> application thta is executed entirely on the client(browser)
 * -> Routs:different URL correseponds to differetn views
 
 > ->User clicks router link -> URL is chnaged(In react,react-router package does this job)-> DOM is updated:react component corresponding to the new URL is rendered[when ever needed it can load data from web API]

 * -> JavaScript (React) is used tyo udpate the page(DOM)
 * -> The page is never reloaded(entire app is juts one page so without any hard reloads)

## Styling option in react

1. inline CSS using using style prop with local scope
2. css or Scss file using className prop with entire app as scope
3. css modules using className with component as scope
4. CSS-in-JS using creating new component scopped component and based in JS
5. tailwind using className prop scoped JSX element
6. using UI library MUI,Chakra UI mantine

> to use global in module.css

```
    :global(.test) {
    background-color: red;
    }
```

## THE URL FOR STATE MANAGEMENT

- The URL is an exceleent place to store UI state and an alternative to useState in some situaltion .Example: open/close panels,currently selected list item,list sorting order,applied list filter

### reasons

1. Easy way to store state in a global place,accessible to all component in the app
2. good way to pass date from one page into the next page
3. make it possible to bookmark and share the page with the exact UI state it had at the time

> www.example.com[/app/cities](path)/[lisbon](param)?[lat=38.728&lng=-9.141](query string)

> path -> corresponds to component currenlty displayed

> param(parameter) -> pass data to next page

> query string -> useful to store some global state that should be accessible everywhere


## Programmatic navigation

- to move to new URL without the user having to click on any link
- use case: right after submitting form


## CONTEXT API (Advance state management)

### a solution to prop drilling

- context API basically allows components everywhere in the tree to read state that a context shares.
- system to pass data throughout the app without manually passing props down the tree
- allows us to " boardcast" global state to the entire app
 1. Provider: gives all child component access to value

  > 1: create a new content

  ```
   const PostContext = createContext();
  ```

  2. Value: data we want to make available(usually state and function)

  > 2: provide value to child component

  ```
    <PostContext.Provider
      value={{
        posts: searchedPosts,
        onAddPost: handleAddPost,
        onClearPosts: handleClearPosts,
        searchQuery,
        setSearchQuery,
      }}

  ```

  3. consumers: all component that read the provided context value

  > 3: consuming the content value

  ```
    const { onClearPosts } = useContext(PostContext);
  ```


> whenever the content value changes/updated all consumers will be automatically re-rendered

> value is updated -> all consumer re-renders(a new way of re-rendering components)


## Review: what is state management

- giving each peice of state the right home

### Types of state

1. state accessibility

- local state : needed only by one or few component, only accessible in component and child component
- global state: might needed by manuy component,accessible to every component in the application

> if this component was rendered twice should a state udpate in one of them reflect in the other one ? global : local

2. state domain

- remote state: all application data loaded from a remote server(API),
  usually asynchronous,need re-fetcheding+updating
- UI state: everything else(theme,list, filtered, form, data, etc),usualy synchronous and stored in the application

### state placement options

- Local component: useState,useReducer,userRef : local state
- parent component: useState,useReducer,userRef : lifting up state
- content : Content API +useState or useReducer : Global state(Prefereably UI state)
- 3rd-party library: Redux,React Query, SWR, Zustand,etc : Global state(remote or UI)
- URL: React Router : Global state,passign between pages
- Browser : Local storrage ,sessionstoreage etc : stpring data in user's browser

### state management tool options

## State Management Matrix

|                  | **Local State**                                                       | **Global State**                                                                             |
| ---------------- | --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **UI State**     | `useState`, `useReducer`, `useRef`                                    | Context API + `useState` / `useReducer`, Redux, Zustand, Recoil, React Router                |
| **Remote State** | `fetch` + `useEffect` + `useState` / `useReducer` _(small apps only)_ | React Query, SWR, RTK Query _(preferred)_ + Redux/Zustand/Recoil (if needed for global sync) |

## PERFORMANCE OPTIMIZATION TOOLS

-> Prevemt wasted renders

- memo (component)
- useMomo(object, function)
- useCallback
- Passing elements as childrene or regular prop

-> Improve App Speed/Responsiveness

- useMemo
- useCllback
- useTransition

-> Reduce Bundle Size

- using fewer 3rd party packages
- code splitting and lazy loading

## WHEN DOES A COMPONENTS INTENCE RE-RENDER?

-> A component instance only re-renders in 3 different situation

- state change
- content change
- parent component re-rendering

> prop change doesnt case re-render as it only happen when parent re-render,henc parent re-render creates the false impression that changing props re-renders a component which is false

### Remember: A render does not mean that the DOM actually gets updated,it just means the component function gets called,But this can be an expensive operation

### WASTED RENDER

-> a render that didn't prodced any change in the DOM
-> only a problem when they happen too frequently or when the component is very slow


## What is MEMOIZATION

> Memoization: Optimizing technique that executes a pure function once,and save the result in memory.If we try to execute the function again with same argument as before,the previosly saved result will be returned,without executing the function again

-> Memorise components with memo
-> Memorise objects with useMemo
-> Memorise function with useCallback

-> Prevent wasteed renders
-> improve app speed/responsiveness

### THE MEMO FUNCTION

-> Used to create a component that will not re-render when its parent re-render as long as the props stays the same between renders
-> Only affects props! A memorized component will still re-render when its own state changes or when a context that it's subscribed to changes
-> Only makes sense when the component is heavy(slow rendering),re-render often and does so with the same props

### AN ISSUE WITH MEMO

> In react,everything is re-rendered on every render(including objects and function)

> In JavaScript, Two objects or function that look the same ,are actually different({}!={}) because they are compared by reference, not by their content

- therefore

-> If object or function are passed as props ,the child component will always see them as new props on each re-render
-> If props are different between re-renders,memo will not work

- Solution

-> We need to memorize objects and function ,to make them stable (preserve) between re-render(memorized{}== memoized {})

### useMemo & useCallback

-> Used to memoized value(useMemo) and function (useCallback) between renders

-> Values passed into useMemo and useCallback will be stored in memory ("cache") and returned in subsequent re-render as long as dependencies ("input") stayes the same

-> useMemo and useCallback have a dependency array(like useEffect): whenever one dependecy changes the value will be re-created

### THREE BIG USE CASES

> useMemo and useCallback is only used in only these 3 cases

- Memoizing props to prevent wasted render(together with memo)
- Memoizing value to avoid expensice re-calcualtions on every render
- Memoizing values that are used in dependency array of another hook

> state setter functions are automaticlly memoized,you can exclude them from dependecy array

### Optimizing Context Re-renders

- Your need to optimise the Context when these 3 things are true at the same time

-> State in the Context needs to change all the time
-> Contenxt has many consumers
-> The app is slow and laggy

1. pass children
2. memoize direct decendent of the context

## DONT OPTIMIZE PREMATURELY

### Don't !
> Dont optimize premeturely
- Dont optimize anything if there is nothing to optimize
- Dont wrap all component in memo(),useMemo(),useCallback()
- Dont optimize content if it is not slow and doent have many consumers

### Do
> Fine performance bottleneck using the profiler and visual inspection(Laggy UI)
- Fix those real performamce issues
- memoize expensive re-renders,calcualation
- Optimize content if it has many consumers and chnages often
- Memoize contexr value + child component
- Implement code splitting + lazy loading for SPA routes

## USEEFFECT DEPENDENCY ARRAY RULES
-> Every single variable ,prop, and context value used inside the effect MUST be included in the dependency array
-> All " reactive values" must be included! That means any finction or varibale that refrences to any othe reacative value
 - Reactive value: state,prop, or context value or anything other that reference a reactive value
-> Dependencies choose themselves: NEVER ignore the exhaustive-deps ESLint rule!
-> Do not use Objects or array as dependencies (Object are recreated on each render ,and React sees new object as different, {} !== {}  react compare with ===)
> Same rules apply to the depndency arrays of other hooks: useMemo and useCallback

## REMOVING UNNESCESSARY DEPENCENCIES
-> removing function dependencies
 - Move function into the effect
 - if you need the function in multiple places ,memoize it(useCallback)
 - if the function doesnt reference any reactive value,move it out of the component
-> removing object dependencies
 - insted of including the entire object including only the properties you need(primitive values)
 - if that doesnt work use the same statergies as of function(moving or memoizing object)
-> Other statergies
  - If you have multiple related values as dependencies try using a reducer(useReducer)
  - you dont need to include setState(from useState) and dispatch(from useReducer) in the dependencies, as react gaurantees them to be statble across render

## WHEN NOT TO USE AN EFFECT
-> effect should be used as a last resort,when no other solution makes sense.React calls them an " escape hatch" to step outside of react

## THREE CASES WHERE EFFECTS ARE OVERUSED(Avoid these as a beginner)
1. Responsing to a user event. An event handler finction should be used instead
2. Fetching data on component mount.This is fine in small app but in real world app a libery like react query should be used
3. Synchronizing state changes with oen another(setting state based on another state varibale) try to use derived state and event handlers
> But everything is accecttable in certain situation and certain doses

## CLOUSERS IN EFFECTS
> A function captures all the varibales from its lexical scope.(FROM THE PLACE IT WAS DEFINED ,AT THE TIME THAT FUNCTION WAS CREATED)
> stale clouser only happnes when if the function is still referencing some oldf value that are outdated by the time this function ins running 

# REDUX
-> 3rd party library to manager global state in web application
-> stand alone liberary,but easy to integrate with react apps using react-redux library
-> All golbal state is stored in on globally accessible store,which is easy to update using "action"(like useReducer)
> Global store is updated -> All consuming component re-render

> It's conceptually similar to using the Context API + useReducer
- You need to0 have a really good understanding for the useReducer hook in order to understand Redux
-> Two versions
  - Classic Redux
  - Modern Redux toolkit

## DO YOU NEED TO LEARN REDUX
-> Historically, Reux was used in most React apps for all golbal state.Today, that has chnaged,because there are many alernatives.Many apps don't need redux anymore,unless they need a lot of global UI state

## THE MECHANISM OF THE USEREDUCER HOOK
- useReducer
Event handler in component -> dispatch -> reducer(current state) -> next state -> re-render
- redux
Event handler in component -> Action creator function(function  creating actions) -> dispatch -> STORE(reducer, reducer ,...,Current State) -> next state -> re-render
> Action creator function: to automate writing action.Helpful to keep all possible actions in one center place(This is convention not a must)

> All global state lives in this centralised container.it's the single source of truth of global state in the app

> Each reducer is a pure finction that calculate the next state(state transition) based on the action and the cirrent state.Usually one reducer per app feature

## WHAT IS REDUX MIDDLEWARE?
> Where to make an asynchronous API call (oor any other async operation in redux)
> STORE -> (No asynchronous operation, reducer needs to be pure function)

> Fetching data inside component is not ideal

# THUNK
Middleware: A Function that ist between dispatching the action and the store.Allows us to run code after dispatching ,but before reaching the reducer in the store
> Perfect for asynchronous code, API calls, timer loggins, side effects
- we use 3 rd party component in this case Thunk(most popular)


## What is Redux Toolkit(RTK)?

-> the morden and preferred way to of writing Redux Code
-> An opinionated approach,forcing us to use redux best practices
-> 100% compatible with "classic" Redux allowing us to use them together
-> Allows us to write a lot less code to achieve the same result

- We can write code that "mutates" state inside reducer(will be converted to immutable logic behind the scenes by "Immer" library)
- Action creators are automatically created
- Automatically setup of thunk middleware and DevTools



```
    import { configureStore } from "@reduxjs/toolkit";
```

> configure store function basically wraps around create store and adds a few fucntionalities to it,it automatically will combine our reducers,add the thunk middleware,setup developer tools

```
  import { createSlice } from "@reduxjs/toolkit";
```

> it'll automatically create action creators from our reducers.Second, it makes writing these reducers a lot easier because we no longer need that switch statement and also the default case is automatically handled.And third, we can actually mutate now,our state inside reducers.

## Redux vs Context API

### Context API + useReducer

1. built into react
2. East to set up a single context
3. Additional state "slide" requires new content set up from scrach("provider hell" in App.js)
4. No mechanism for asynch operation
5. performance opetimization is a pain
6. Only React DevTool

### When to use Context API + useReducer

-> Use Context API for global state management in small apps

- When you just need to share a value that doesnt change often(color theme,language authenticate user..)
- When you need toslve simple prop drilling problem
- when you need to manage state in a local sub-tree of the app
  > example in the compound component pattern

### Redux

1. Require additional packages(larger bundle size)
2. more work to set up initially
3. once set up,it is easy to create additional state "slices"
4. supporst middleware for async operations
5. performance is optimized out of box
6. Excellent DevTool

### When to use redux

-> use Redux for global state management in large apps

- When you have lots of global UI state that needs to be updated frequently(beacause redux is optimized for this){shopping cart,current atb,complex filters or search...}
- When you have complex state with nested objects and array(beacause you can mutate state with redux toolkit)
  > these are not super common in UI state


# How to Plan and Built A react Application

- for Small apps with one page and a few features
  1. Break the desired UI into components
  2. Build a static version(no state yet)
  3. Think about the state management+data flow
- IN REAL WORLD APPS(Rough overview)
  1. Gather application requirements and features
  2. Divide the application into pages
     - Think about overall and page-level UI
     - Break the desired UI into components
     - Design and build a static version (no state yet)
  3. Divide the application into feature categories
     - Think about state management + data flow
  4. Decide on what library to use(Technology decision)

# Styles Components

> let's us write css in javascript component file

```bash
 npm i styled-components
```

```bash
import styled from "styled-components";

const H1 = styled.h1`
  font-size: 30px;
  font-weight: 600;
`;

<H1>The Wild Oasis</H1>
```

- styled return a react component

> downlode this extention -> vscode-styled-components

- to style the preexixting App component

```bash
  const StyledApp = styled.div`
  background-color: orangered;
  padding: 20px;
`;
```

- to create global styles create a GlobalStyles.js file and pase the global css inside this

```bash
const GlobalStyles = createGlobalStyle``;
export default GlobalStyles;
```

> to include this in application come to App.js,GlobalStyles needs to be added in the component tree but it cannot accept any children we want this to be sibling of StyledApp

```bash
    <>
      <GlobalStyles />
      <StyledApp>
        <H1>The Wild Oasis</H1>
      </StyledApp>
    </>
```

> Advance usage is styled component ins theming by exporting ThemeProvider wrapper component which provied a theme to all react components underneath itself via the content API

- styled component props and css function

```bash
 <Heading as="h2">The Wild Oasis in h2</Heading>
```

```bash

/* eslint-disable no-unused-vars */
/* eslint-disable no-constant-condition */

import styled, { css } from "styled-components";

// const text = css`
//   text-align: center;
//   ${10 > 5 && "background-color: yellow;"}
// `;

const Heading = styled.h1`
  ${(props) =>
    props.as === "h1" &&
    css`
      font-size: 3rem;
      font-weight: 600;
    `}

  ${(props) =>
    props.as === "h2" &&
    css`
      font-size: 2rem;
      font-weight: 500;
    `}

      ${(props) =>
    props.as === "h3" &&
    css`
      font-size: 1.5rem;
      font-weight: 400;
    `}
  line-height:1.4
`;

export default Heading;

```

- you can set a default type to any react component like this

```bash
  const Row = styled.div`
    display: flex;
    ${(props) =>
      props.type === "horizontal" &&
      css`
        justify-content: space-between;
        align-items: center;
      `}

    ${(props) =>
      props.type === "vertical" &&
      css`
        flex-direction: column;
        gap: 2rem;
      `}
  `;

  Row.defaultProps = {
    type: "vertical",
  };
```

## What is SUPABASE

- Service that allows developers to easily creaste a back end with a postgres database
- Automatically creates a database and APIU so we can easily request and receice data from the server
- no bacend development needed
- supabase also comes with easy-to-use user authentication and file storage

### Modeling State

| State / Domain | Feature Categories                       |
| -------------- | ---------------------------------------- |
| Booking        | Bookings, Dashboard, Check-in, Check-out |
| Cabins         | Cabin Management                         |
| Guests         | Guest Management                         |
| Settings       | Application Settings                     |
| Users          | Authentication & User Management         |

- All this satet will be global remote state ,stored withing Supabase
- There will be on table for each state "Slice" in the database

### The Bookings Table

- Bookings are about a guest renting a cabin
- So a boookins needs information about what guest is booking whihc cabin:we need to connect them
- Supabase uses a Postgres DB,whihc is SQL (relational DB),So we join tables using foreign keys(guestID,CabinId)

Booking > id,guestId,cabinId,....
Guest > id,email,...
Cabin > id, name,...

> We connect a booking with a cabin by storing the cabin;s id(primary key) inside the booking cabin Id(Foreign key)

## React Query (TanStack Query )

- Powerful library for managing remote(server) state
- Many features that allows us to write a lot less code,while also making the UX a lot better

1. Data is stored in a cache
2. Automatic loadinh and error state
3. Automatic re-fetching to keep state synced
4. pre-fetching(pagination - fetching data of next pages with current page)
5. easy remote state mutation(updating)
6. offline support

- Needed becaused rempote state is fundamentally differently from regular UI state
- other tools: SWR, Reduc, RTK, but RQ is most popular

- installation react query

```bash
npm i @tanstack/react-query@4
```

- installing react dev tools

```bash
npm install @tanstack/react-query-devtools@4
```

- setting

```bash
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: 60 * 1000,
    },
  },
});

<QueryClientProvider client={queryClient}>
  <ReactQueryDevtools initialIsOpen={false} />
  <GlobalStyles />
  <BrowserRouter>
    <Routes>
      <Route element={<AppLayout />}>
        <Route index element={<Navigate replace to="dashboard" />} />
        <Route path="account" element={<Account />} />
      </Route>
      <Route path="login" element={<Login />} />
      <Route path="*" element={<PageNotFound />} />
    </Routes>
  </BrowserRouter>
</QueryClientProvider>
```

## An overview of Reusability in react

### how to reuse code in react

- ui

1. components and props(use props as a component API to enable custom behaviour.Can be stateless ,staeful or structural components)
2. Childrem prop( to cutomize the component's content)

- stateful logic(logic with hooks)

1. custom hooks

## render props pattern

- For complete control over what the component renders,by passing in a function that tells the component what to render.was more common before hooks but still useful

### compound component pattern

- we will have multiple components that play together in order ot create one big super component
- for very self-contained component that need/want to manage their own state.Compound components are like fancy super components

## Render Props Pattern

- passing prop called render which a function that component uses to know what it should render and how to do it.

## Higher-Order Components (HOC)

> what to do if you got a componet form 3rd party lib and you want to implement few designes whihc you created without chaning the components

- A HOC is simply a component taht takes in another component and then return a new component that is better so an enhanced version of the initial component
- its name start with "with" name and it takes a component and returns a new one with additional functinality

### React Portal

- The main reason why a portal becomes necssary is in order ot avoid confilcts with CSS property overflow set to hidden

### peculiarity due to Element flow

> when im clicking outside the Modal it closed but once it is cloed the cabin or show table dont show even after clicking why?

```bash
 const ref = useRef();
  useEffect(
    function () {
      function handleClick(e) {
        if (ref.current && !ref.current.contains(e.target)) close();
      }
      document.addEventListener("click", handleClick);
      return () => document.removeEventListener("click", handleClick);
    },
    [close],
  );

  if (name !== openName) return null;
  return createPortal(
    <Overlay>
      <StyledModal ref={ref}>
```

- when i click button, Event Bubble Up all the way to DOM untill it reaches that Modal Window and os then the click is basically delected outside the modal window which is immediately closed

- dont listen to this events at bubbling state but on capturing state

```bash
  document.addEventListener("click", handleClick,true);
      return () => document.removeEventListener("click", handleClick,true);
```

### transient prop

-A transient prop is a special feature in styled-components that lets you pass props to a styled component without forwarding them to the actual DOM element.It is created by prefixing the prop name with a dollar sign ($).

```bash
<FilterButton active={true}>
  All
</FilterButton>

const FilterButton = styled.button`
  ${(props) =>
    props.active &&
    css`
      background-color: blue;
    `}
`;

```

> Styled-components uses active for styling, but it also forwards it to the HTML button:

```bash
<button active="true">All</button>
```

-Transient prop solution

```bash
<FilterButton $active={true}>
  All
</FilterButton>

const FilterButton = styled.button`
  ${(props) =>
    props.$active &&
    css`
      background-color: blue;
    `}
`;

```

> Now styled-components uses $active internally for styling, but does not pass it to the DOM.

### Error Boundry

> try and catch for react

- catch error only while react is rendering
