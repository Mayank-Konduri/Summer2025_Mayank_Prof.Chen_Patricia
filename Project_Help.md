## June 21st

**Question:** Should I build a ReLU feedforward network with L = Q + 1 layers, where Q is the number of classes (so L = 4 for digits 0, 1, 2), and use gradient descent?  
**Answer:** Yes

---

**Question:** Is it correct that the input layer has dimension d0 = 784, and the hidden layers can have decreasing widths as long as each width is at least Q?  
**Answer:** Yes. I suggest starting with letting all layers have dimension 784, except for the last one, which should have d_L = 10.

---

**Question:** After training, should I compute the cumulative weight matrices W_l and bias vectors b_l using the recursive formulas: W_l = W_l * W_{l-1} * ..., and b_l = W_l * b_{l-1} + b_l?  
**Answer:** Yes

---

**Question:** Once I have W_l and b_l, do I apply the truncation map tau_{W, b}(x) = W_pseudoinverse (ReLU(Wx + b) - b) at each layer?  
**Answer:** After the network is trained, you don't need to apply the truncation maps, as the neural network is already implementing a truncation map with some cones. **

---

**Question:** To extract the cone geometry, should I compute the base point as p = -W_pseudoinverse * b and the edge vectors as v_i = W_pseudoinverse * e_i, where e_i are standard basis vectors?  
**Answer:** Yes

---

**Question:** Finally, I'm guessing I should use PCA to project the data and cone structures into 2D or 3D space, and then visualize how the data transforms layer-by-layer?  
**Answer:** Initially I was just thinking to have a look at what the cones look like, maybe superimposed with the initial data. It would be very cool to also have a graphic visualization of the cones transforming the data, but that can come later.

---

**Note:**  
** After you get the cumulative weights and biases, you can assume that the neural network is applying every truncation map tau_{W^(l), bˆ(l)} on the data, one after the other. So the first layer does tau_{W^(1), bˆ(1)}, the second layer does tau_{W^(2), bˆ(2)} and so on, up until the last layer when everything gets mapped to the output (that's the content of equation (3.7) here). 

The action of each of these truncation maps is given by the corresponding cone. So for the first cone, you would compute p = -W^(1)_pseudoinverse * b^(1) and v_i = W^(1)_pseudoinverse and similarly for the other cones.
