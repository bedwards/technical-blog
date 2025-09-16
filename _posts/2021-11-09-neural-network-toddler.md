---
---
# Building a Neural Network Feels Like Teaching a Toddler Calculus

When I first implemented backpropagation from scratch, I had this moment where I realized neural networks are basically just very expensive ways to approximate functions. You're essentially telling the computer "here's a bunch of examples, figure out the pattern" and hoping it doesn't just memorize everything like that one student who could recite the textbook but couldn't solve a single novel problem.

The thing that kills me about modern deep learning is how we've collectively agreed to pretend we understand why batch normalization works. Sure, we have these hand-wavy explanations about internal covariate shift, but really we just know it makes training more stable and we're all too afraid to question it. It's like how medieval blacksmiths knew that quenching steel in urine made better swords - they had theories about spirits and essences, but really they were just accidentally adding nitrogen. We're doing the same thing with neural networks, just with fancier math.

My favorite part of training models is watching the loss curve and trying to diagnose what's going wrong from its shape. That sudden spike at epoch 47? Your learning rate is too high and you just catapulted over a minimum. That plateau that looks like Kansas? You're stuck in a saddle point and need to add some noise. That perfect exponential decay that suddenly explodes? Congratulations, you've encountered the dreaded gradient explosion, and your weights are now NASA's problem because they've achieved escape velocity.

---

I am working on copying all my blog posts to LinkedIn. In the meantime, you can find them all at

[https://bedwards.github.io/technical-blog/](https://bedwards.github.io/technical-blog/)

After re-reading this post, I am motivated to explain the concepts from first principles, differentiating them from similar concepts (or their opposites).

---

When you train a neural network, each layer passes numbers (activations) to the next. These numbers can be spread out in all kinds of ways: sometimes small, sometimes large, sometimes bunched around zero, sometimes drifting far away. If the spread shifts from one batch of data to the next, the later layers keep having to re-learn how to deal with them. That constant shifting is what people mean by internal covariate shift: the inputs to each layer are not stable, they keep changing as the network learns.

Batch normalization is a trick to stabilize this. Instead of letting each layer’s outputs wander off wherever they like, you stop, look at a batch of data, and rescale it. For each neuron, you take the outputs across the batch, compute their average and their spread, then normalize them: subtract the average, divide by the spread. That gives you a more stable, predictable distribution—numbers roughly centered at zero, with similar scale. Once you have this stable base, you let the network learn two simple adjustments per neuron: a scale and a shift. That way, if a layer really wants its outputs stretched or shifted, it can still learn that, but now it’s controlled, not chaotic. The effect is like keeping the training process on even ground. Gradients flow more smoothly, learning speeds up, and training becomes more stable.

Now shift metaphors. Training a network is like wandering through a mountain range at night, trying to find the lowest valley. The “loss curve” is your altimeter. It tells you how high you are—how bad your predictions are. A high loss means you’re stranded on a peak, far from where you want to be. A low loss means you’ve descended closer to the valley floor, where the model actually works. Plotting the loss as you go shows whether you are steadily making progress downhill, stuck on a ledge, or climbing back up by mistake.

The “learning rate” is your stride length. Take steps that are too small, and you’ll crawl endlessly without reaching the valley. Take steps that are too big, and you’ll stumble past the valley and ricochet around wildly. Choosing or adjusting the stride length is crucial.

Consider a saddle point. It looks like a pass in the mountains: sloping downward in one direction, upward in another, and almost flat in between. If you’re crossing it blindly, progress feels agonizingly slow. Networks often drift in these flat regions, wandering without improvement. One remedy is to add a little noise—random nudges that jostle you out of indecision and set you moving downhill again.

Another is to change how you step. Early on, bold strides help you cover ground quickly. But as you near the valley floor, caution matters more. Exponential decay of the learning rate is one way to achieve this: it gradually shrinks your stride so that you don’t overshoot or undo your own progress.

And then there is the opposite problem: not hesitation, but violent motion. Gradient explosion happens when the slope is measured as impossibly steep, and the network’s update multiplies into a leap so huge it hurls you out of the valley entirely. Training collapses, numbers shoot off to infinity, nothing makes sense. The cure is to clip the stride—to limit the maximum step you can take, no matter how intense the slope seems.

Together, these ideas—batch normalization, loss curves, learning rates, saddle points, noise, exponential decay, and guarding against explosion—are all variations on the same theme. They are ways of making a difficult nighttime descent through mountains possible. They give you a steadier map, a calmer stride, and a path toward the valley where the network finally learns.