# Reset-Synchroniser-in-Verilog
De-asserting reset signal can cause metastability. This module fixes that, by asserting reset asynchronously and de-asserting it synchronously

## The problem in depth
The main drawback of employing an asynchronous reset lies in the de-assertion phases of the signal. If the asynchronous reset de-asserts close to an active clock edge, the flip-flop's output may enter a metastable state, violating the flip-flop's setup and hold time. Consequently, the flip-flop may transition to an unknown state, leading to unpredictable outcomes.

To mitigate this risk, a reset synchronizer is employed to manage the de-assertion of the reset circuit and prevent metastability. Synchronization of the reset’s de-assertion on a specific clock domain requires a shift register of at least 2-3 flip flops. If the de-assertion of the reset of a synchronous element occurs near a CLK active edge, metastability occurs; however the second flip flop in the chain remains stable at 0, since the input and output are both low, preventing any output change due to the input that might occur when a reset is removed.
