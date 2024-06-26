from typing import *;
from math import *;
from tailors import *;
from floating_point_error_fixer import cut_floating_point_to_precision;



def dbp(n, h, target_x, current_x, current_y, previous_x, previous_y):
	msg:str = f"""
	n={n}
	h={h}
	target_x={target_x}
	current_x={current_x}
	current_y={current_y}
	previous_x={previous_x}
	previous_y={previous_y}
	"""
	print(msg);


def solve_by_tailor_3rd(target_x:float, y:float, x:float, h:float, f, f_, f__)->float:
	n:int = 0;
	current_x:float = 0;
	current_y:float = 0;
	previous_x:float = x;
	previous_y:float = y;
	while True:
		current_x = x + (n * h);

		current_y = tailor_3rd(
			previous_y, 
			previous_x, 
			h,
			f,
			f_,
			f__,
			);

		current_y = cut_floating_point_to_precision(current_y);

		dbp(
			n,
			h,
			target_x,
			current_x,
			current_y,
			previous_x,
			previous_y,	
			);

		if (current_x >= target_x):
			print(f"found f({current_x})={current_y}");
			return current_y


		previous_x = current_x;
		previous_y = current_y;
	


		n += 1;








if __name__ == "__main__":
	def f(x:float, y:float)->float:
		return x*sin(y)+1;

	def f_(x:float, y:float)->float:
		return -x*sin(y);

	def f__(x:float, y:float)->float:
		return cos(y)**2;

	solve_by_tailor_3rd(
		target_x=0.1, y=0, x=0, h=0.1, f=f, f_=f_, f__=f__
		);


