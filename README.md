# RIPLLE-COUNTER

Design code:

module ripple_counter(
    input clk,
    input rst_n, 
    output [3:0] q
);
    reg [3:0] q_reg;
    
    always @(posedge clk or negedge rst_n) begin
        if (!rst_n) begin
            q_reg <= 4'b0000; 
        end 
        else 
        begin
            q_reg <= q_reg + 1; 
        end
    end 
    assign q = q_reg;
endmodule

Test bench:

module tb_ripple_counter;
    reg clk;
    reg rst_n;
    wire [3:0] q;
    ripple_counter uut (
        .clk(clk),
        .rst_n(rst_n),
        .q(q)
    );
    always #5 clk = ~clk;
    initial begin
        clk = 0;
        rst_n = 0;
        #10 rst_n = 1;
        #100;
        $finish;
    end
    initial begin
        $monitor("At time %t, q = %b", $time, q);
    end
endmodule

