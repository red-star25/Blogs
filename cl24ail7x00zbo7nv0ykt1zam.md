---
title: "Bloc Concurrency: Advance Event Transformer"
datePublished: Mon Apr 18 2022 05:42:18 GMT+0000 (Coordinated Universal Time)
cuid: cl24ail7x00zbo7nv0ykt1zam
slug: bloc-concurrency-advance-event-transformer
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1650192130684/2Z5gWh7rS.png
tags: programming-blogs, programming, dart, flutter, concurrency

---

## Event Transformation
- To retrieve data/state in BloC, we use the UI to trigger/pass an event to the BloC. When we're not working with real-time apps, this is OK.
- However, in some cases, we don't want our user to send the same request to the server many times in order to avoid hitting the rate limit and save money/load on the backend.
- We'll need some type of control over the Event inside our BloC for this.
- This is where the event transformation concept comes into play.
- Consider the following code as an example to better grasp this concept:
```
class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc() : super(0) {
    on<IncrementCounterEvent>(
      (event, emit) async {
        await Future<void>.delayed(const Duration(seconds: 1));
        emit(state + 1);
      },
    );
    on<DecrementCounterEvent>(
      (event, emit) async {
        await Future<void>.delayed(const Duration(seconds: 1));
        emit(state - 1);
      },
    );
}
```
- In the preceding code, we are just transmitting the relevant state whenever the user presses the Increment or Decrement button.
- But there's a catch: we're waiting **1 second** before emitting a new state.
- Let's go on to the CounterPage now. Consider the code below.
```
Future<void> tick() => Future<void>.delayed(Duration.zero);
class CounterHome extends StatelessWidget {
      const CounterHome({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("Counter")),
      floatingActionButton: Row(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          FloatingActionButton(
            onPressed: () async {
              context.read<CounterBloc>().add(IncrementCounterEvent());
              await tick();

              context.read<CounterBloc>().add(IncrementCounterEvent());
              await tick();

              context.read<CounterBloc>().add(IncrementCounterEvent());
              await tick();

              context.read<CounterBloc>().add(IncrementCounterEvent());
              await tick();

              context.read<CounterBloc>().add(IncrementCounterEvent());
              await tick();

              context.read<CounterBloc>().add(IncrementCounterEvent());
            },
            child: const Icon(Icons.add),
          ),
          const SizedBox(width: 8),
          FloatingActionButton(
            onPressed: () async {},
            child: const Icon(Icons.remove),
          ),
        ],
      ),
      body: BlocBuilder<CounterBloc, int>(
        builder: (context, state) {
          return Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                const Text(
                  'You have pushed the button this many times:',
                ),
                Text(
                  '$state',
                  style: Theme.of(context).textTheme.headline4,
                ),
              ],
            ),
          );
        },
      ),
    );
  }
}
```
- The user interface is straightforward; we're simply displaying the state of the CounterBloc, which is of type **int**.
- One floating button is used to update the counter's current state.

![counter ui.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650180882143/pH9IXGmQJ.png)

- Now I'll ask you a question: What happens if I push the Plus(+) button?

![btn click.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1650181116016/VRQX9IfFq.gif)

- After one second has passed, all of the events will be executed immediately. What's going on here? But didn't we say there would be a one-second delay? You are correct; we did. Lets see what's happening here.

## Transformer
- Prior to BloC v.7.2.0, you had to use Cubit to perform your event sequentially.
- However, you no longer need to use Cubit for this; you can just apply the change from within your Bloc.
- To perform different transformations, we'll use the [bloc concurrency](https://pub.dev/packages/bloc concurrency) package.
- You can even build and provide your own transformer to the bloc. But, for the sake of simplicity, I'm going to utilise this package.
- Go to our CounterBloc and provide the `transformer` parameter to the 'onCounterEvent>()' method.
- Here, use the bloc concurrency package's `sequential()` transformer to add the `sequential()` transformer to the event.
```
class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc() : super(0) {
    on<IncrementCounterEvent>(
      (event, emit) async {
        await Future<void>.delayed(const Duration(seconds: 1));
        emit(state + 1);
      },
      transformer: sequential(),
    );
    on<DecrementCounterEvent>(
      (event, emit) async {
        await Future<void>.delayed(const Duration(seconds: 1));
        emit(state - 1);
      },
      transformer: sequential(),
    );
  }
```
- Now let's execute the code to test whether it works as planned.

![no.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1650188965452/NHsrIchjS.gif)
- As you can see, it's still not working; we want our events to execute in sequence, one after the other. Didn't we, however, pass the transformer? So, why isn't this working?
- The problem is that the above code will not make Bloc act as we wanted!
- Events are categorised into buckets based on how they are registered.
- This means that all of the events you wish to perform in sequence should be in the same Event bucket. In our case, we've divided the events into two buckets:
 - IncrementCounterEvent() and
 - DecrementCounterEvent()
- If you need your blocs to behave purely sequentially, you'll have to register a single bucket to catch all of the events.
- So how can we achieve this? Well, it's simple. Consider the below code
```
class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc() : super(0) {
    on<CounterEvent>(
      (event, emit) async {
        await Future<void>.delayed(const Duration(seconds: 1));
        if (event is IncrementCounterEvent) {
          emit(state + 1);
        } else if (event is DecrementCounterEvent) {
          emit(state - 1);
        }
      },
      transformer: sequential(),
    );
  }
```
- As you can see, we just have one Event bucket now, which is `CounterEvent`.  The rest of the logic stays unchanged.
- It should now work if you execute the code.

![working.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1650189792500/wXkTu8f0X.gif)
- As you can see, now the events are running sequentially: 0,1,0,1,0.....

-------
- This is one of the transformer we saw from the `bloc_concurrency` package. There are other transformers too. If you want to learn about other transformer checkout it's github.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650190006665/rbi4hrSeh.png)
- You can also create your own transformer and transform your event as you want.

-------
## Wrapping Up
- **That concludes my remarks. I hope you grasped the fundamental concept of concurrency. Make one example and try to put that into practice on your own. Then you'll have a better understanding of how to use it and where to use it.**
- **I hope you enjoyed and learned something from this article. If you have any feedback/queries, leave them in the comments.**
- **Thank you for spending time reading this article. See you in the next article. Until then...**

![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1650190975920/y9LMlCh9Q.gif)

-------
- Follow me on [LinkedIn](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), [Twiiter](https://twitter.com/dhruv_nakum), [Github](https://github.com/red-star25) for more updates