`timescale 1ns / 1ps

module Seq_Recog_Module( x0, x1, clk, rst, out, rtrn

    );

	 input x0;				//Coming Input
	 input x1;

	 input clk;			//Clock 
	 input rst; 

	 output reg out;	//Output
	 output reg rtrn;	//Output

	 int flag = 0;


//Evolved circuit startes from here

    reg [2:0]state; 
    parameter S0 = 3'b000; 
    parameter S1 = 3'b001; 
    parameter S2 = 3'b011; 
    parameter S3 = 3'b010; 
    parameter S4 = 3'b110; 
    parameter S5 = 3'b100;

    always @(posedge clk) begin 
        if(!rst) begin 
            if (state == S2) begin 
                if (x1 == 0) begin 
                    state = S4; 
                    out = 1; 
                    rtrn = 0; 
                end 
                else if (x1 == 1) begin 
                    state = S3; 
                    out = 1; 
                    rtrn = 1; 
                end 
                else begin 
                    state = S5; 
                    out = 0; 
                    rtrn = 0; 
                end 
            end 
            else if (state == S1) begin 
                if (x1 == 1) begin 
                    state = S5; 
                    out = 1; 
                    rtrn = 0; 
                end else if (x0 == 1) begin 
                    state = S0; 
                    out = 0; 
                    rtrn = 1; 
                end 
                else begin 
                    state = S2; 
                    out = 0; 
                    rtrn = 0; 
                end 
            end 
            else if (state == S0) begin 
                if (x1 == 1) begin 
                    state = S4; 
                    out = 1; 
                    rtrn = 1; 
                end else if (x0 == 1) begin 
                    state = S3; 
                    out = 0; 
                    rtrn = 0; 
                end else begin 
                    state = S1; 
                    out = 0; 
                    rtrn = 0; 
                end 
            end 
            else if (state == S0) begin 
                if (x1 == 1) begin 
                    state = S0; 
                    out = 0; 
                    rtrn = 1; 
                end 
                else if (x0 == 0) begin 
                    state = S1; 
                    out = 0; 
                    rtrn = 1; 
                end 
                else begin 
                    state = S5; 
                    out = 0; 
                    rtrn = 1; 
                end 
            end 
            else if (state == S5) begin 
                if (x1 == 0) begin 
                    state = S3; 
                    out = 0;
                    rtrn = 0; 
                end 
                else if (x1 == 0) begin 
                    state = S4; 
                    out = 0; 
                    rtrn = 0; 
                end 
                else begin 
                    state = S4; 
                    out = 0; 
                    rtrn = 0; 
                end 
            end 
            else if (state == S3) begin 
                if (x0 == 0) begin 
                    state = S5; 
                    out = 0; 
                    rtrn = 0; 
                end 
                else if (x1 == 1) begin 
                    state = S2; 
                    out = 0; 
                    rtrn = 0; 
                end 
                else begin 
                    state = S1; 
                    out = 0; 
                    rtrn = 0; 
                end 
            end
            else begin 
                state = S0; 
                out = 0; 
                rtrn = 0; 
            end 
        end 
        else begin 
            state = S0; 
            out = 0; 
            rtrn = 0; 
        end 
    end
    

