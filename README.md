This is the README for my Optimization Module in DCS340.
This file includes information about each of the programs included in this repo, as well as short a short reflection on the process of creating each program.

## Programs

| Notebook | Methods | Problem |
|---|---|---|
| `ClassicOptDemo.ipynb` | Guess and check, gradient ascent | Maximize f(x) = 4 − (x − 2)² |
| `Bisection_Newtons_demo.ipynb` | Bisection, Newton's method, multi-start Newton's method | Find maxima by solving f'(x) = 0, including a wavy function with many local peaks |
| `2DInputs.ipynb` | Nelder-Mead, gradient descent, Newton's method (with the Hessian) | Minimize f(x, y) = (x − 2)² − xy + (y − 3)² |

## How to run

The notebooks need Python 3 with `numpy`, `matplotlib`, and `scipy` (`scipy` is only used for Nelder-Mead in `2DInputs.ipynb`).

- **VS Code:** clone the repo, open a notebook, pick a Python kernel, and click **Run All**.
- **Google Colab:** open a notebook from GitHub with **File → Open notebook → GitHub** and paste this repo's URL.

```bash
git clone https://github.com/LiamBaron5/DCS340_OptimizationModule.git
pip install numpy matplotlib scipy
```

---------- Reflections ----------
## ClassicOptDemo.ipynb — Guess and Check & Gradient Ascent

This program was my introduction to optimization, using the simple parabola f(x) = 4 − (x − 2)². Guess and check showed me the most basic way to find a maximum: evaluate the function at a set of points and keep the best one. It worked here, but only because the true maximum at x = 2 happened to be one of my guesses. I realized this approach doesn't scale. With a finer grid, a wider range, or more dimensions, the number of guesses grows very quickly.

Gradient ascent showed me how using the derivative makes a search smarter. Instead of checking everything, it uses the slope to decide which direction to move and how far. I learned how important the step size (learning rate) is, and that getting the direction of the update wrong makes the algorithm move away from the answer instead of toward it. I also saw that for more complex functions, calculating the derivative by hand becomes its own challenge.

## Bisection_Newtons_demo.ipynb — Bisection & Newton's Method

This program taught me that finding a maximum is really a root-finding problem: the maximum is where the derivative equals zero. Bisection was reliable and easy to understand. As long as the starting bracket contains a sign change in the derivative, cutting the interval in half each time always closes in on the answer. The tradeoff is speed, since it took around 20 halvings to get close.

Newton's method was much faster because it uses both the slope (first derivative) and the curvature (second derivative). On the simple quadratic it found x = 2 in a single step. I also learned its weaknesses: it needs the second derivative, and it breaks down when the second derivative is close to zero, so I had to guard against that.

The multi-start section was the most valuable part. On a wavy function with many peaks, a single Newton run just converges to whatever critical point is nearest its starting spot, which could be a local maximum or even a minimum. Running Newton from many starting points, keeping only results where the second derivative is negative, and picking the highest value gave a much better chance of finding the global maximum. I had to increase the number of starting points to get a good result, which showed me that more coverage costs more computation but improves reliability. Plotting every search path made it clear how much the starting point matters.

## 2DInputs.ipynb — Nelder-Mead, Gradient Descent & Newton's Method in 2D

This program extended optimization to two inputs using f(x, y) = (x − 2)² − xy + (y − 3)². Visualizing the function helped me build intuition. The 3D surface showed the overall shape, and the contour plot was even more useful: the center of the "bulls-eye" marks the minimum, and rings that are closer together show steeper areas.

Comparing three methods on the same problem taught me that each has tradeoffs:
- **Nelder-Mead** was the easiest to use because it needs no derivatives. It just moves and reshapes a triangle across the surface. It found the exact minimum at (4.667, 5.333), but it took over 200 function evaluations.
- **Gradient descent** required me to compute partial derivatives by hand. Even after I added more iterations it ended slightly short of the true minimum, and plotting its path showed how gradually it approaches the answer.
- **Newton's method** was the most efficient. Using the gradient and the Hessian matrix, it jumped to the exact minimum in one iteration, because the function is quadratic. The cost is that it needs both first and second derivatives, which would be much harder to get for a complicated function.

Overall, this program showed me that there is no single best optimization method. The right choice depends on how much you know about the function (whether you have derivatives), how accurate you need to be, and how much computation you can afford.

---

This project is part of my portfolio: **https://LiamBaron5.github.io**
