# DE-Hackathon
 ### (i) Teams will have to design a combinational/sequential circuit as the solution for the problem statement.
### Problem solving steps:
Given the requirement to design combinational and sequential circuits for addressing traffic congestion in metropolitan cities, here's a more detailed breakdown of potential circuits:

### Traffic Light Controller:

Combinational logic can be used to determine the optimal timing for traffic signals based on inputs such as traffic flow, pedestrian crossings, and time of day.
Sequential logic can be employed to control the sequence of traffic light changes and to ensure smooth transitions between states.
### Traffic Flow Monitoring:

Combinational circuits can process inputs from sensors detecting vehicle presence and count the number of vehicles passing through.
Sequential circuits can be utilized to store and analyze historical traffic data, identifying patterns and predicting future congestion.
### Traffic Signal Coordination:

Combinational logic can be used to coordinate signals at intersections, ensuring that green lights are synchronized to facilitate continuous traffic flow.
Sequential logic can help maintain the timing of signal changes and adjust them dynamically based on real-time traffic conditions.
### Dynamic Lane Management:

Combinational circuits can control lane direction indicators based on inputs such as traffic volume and congestion levels.
Sequential circuits can manage the switching of lanes, ensuring smooth transitions and preventing collisions.
### Route Optimization:

Combinational logic can be employed to calculate optimal routes based on inputs such as traffic data, road conditions, and distance.
Sequential logic can store and update route information, guiding drivers through the most efficient paths.
### Vehicle Priority Systems:

Combinational circuits can determine priority for vehicles such as emergency vehicles, public transport, and high-occupancy vehicles based on predefined criteria.
Sequential circuits can manage the allocation of priority lanes and signals, ensuring that priority vehicles can move smoothly through traffic.
### Traffic Data Analysis:

Combinational logic circuits can process raw traffic data collected from sensors and detectors, performing tasks such as filtering, sorting, and aggregating.
Sequential circuits can analyze the processed data over time, identifying trends, patterns, and areas of congestion.
### Adaptive Traffic Control:

Combinational logic can be used to design algorithms for adaptive traffic control, which dynamically adjust traffic signal timings and lane configurations based on real-time inputs.
Sequential logic circuits can implement learning mechanisms that adapt the system's behavior over time based on observed traffic patterns and feedback.
### (ii) Final and intermediate outputs of the code/RTL Schematic implementation will be observed and will be given high weightage.
### Verilog Code:
### Developed by: K MADHAVA REDDY
### RegisterNumber: 212223240064
```
module TrafficLightController(
    input clk,
    output reg red1,
    output reg yellow1,
    output reg green1,
    output reg red2,
    output reg yellow2,
    output reg green2,
    output reg red3,
    output reg yellow3,
    output reg green3
);

// State machine definition
parameter S_IDLE = 2'b00;
parameter S_ROAD1 = 2'b01;
parameter S_ROAD2 = 2'b10;
parameter S_ROAD3 = 2'b11;

reg [1:0] state;
reg [3:0] count;

always @(posedge clk) begin
    // State transition
    case(state)
        S_IDLE: begin
            count <= count + 1;
            if (count == 5) begin
                state <= S_ROAD1;
                count <= 0;
            end
        end
        S_ROAD1: begin
            count <= count + 1;
            if (count == 5) begin
                state <= S_ROAD2;
                count <= 0;
            end
        end
        S_ROAD2: begin
            count <= count + 1;
            if (count == 5) begin
                state <= S_ROAD3;
                count <= 0;
            end
        end
        S_ROAD3: begin
            count <= count + 1;
            if (count == 5) begin
                state <= S_IDLE;
                count <= 0;
            end
        end
    endcase
end

// Traffic light control logic
always @(*) begin
    case(state)
        S_IDLE: begin
            red1 = 1;
            yellow1 = (count >= 1 && count <= 4) ? 1 : 0;
            green1 = 0;
            red2 = 1;
            yellow2 = 0;
            green2 = 0;
            red3 = 1;
            yellow3 = 0;
            green3 = 0;
        end
        S_ROAD1: begin
            red1 = 0;
            yellow1 = (count >= 6 && count <= 9) ? 1 : 0;
            green1 = (count >= 1 && count <= 5) ? 1 : 0;
            red2 = 1;
            yellow2 = (count >= 6 && count <= 9) ? 1 : 0;
            green2 = 0;
            red3 = 1;
            yellow3 = 0;
            green3 = 0;
        end
        S_ROAD2: begin
            red1 = 1;
            yellow1 = 0;
            green1 = 0;
            red2 = 0;
            yellow2 = (count >= 1 && count <= 4) ? 1 : 0;
            green2 = (count >= 6 && count <= 9) ? 1 : 0;
            red3 = 1;
            yellow3 = (count >= 6 && count <= 9) ? 1 : 0;
            green3 = 0;
        end
        S_ROAD3: begin
            red1 = 1;
            yellow1 = 0;
            green1 = 0;
            red2 = 1;
            yellow2 = 0;
            green2 = 0;
            red3 = 0;
            yellow3 = (count >= 1 && count <= 4) ? 1 : 0;
            green3 = (count >= 6 && count <= 9) ? 1 : 0;
        end
    endcase
end

endmodule

```

**RTL Schematic**
![image](https://github.com/Madhavareddy09/Project-Based-Experiment/assets/145742470/9531d30f-5762-4055-9cd3-a45c8bc7a86b)

**Output Timing Waveform**

![image](https://github.com/Madhavareddy09/Project-Based-Experiment/assets/145742470/6e37ff28-56cf-49ff-af7b-90be4e960459)









### Result:
The solution for Traffic Congestion in Metro Cities using verilog code are executed Successfully.
