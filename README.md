# data-distribution
For calculating the mean, median and mode for unimodal data from the input list. Then compare the mean, median and mode to get the shape of the unimodal data distribution. The output (shape of distribution) can be "Symmetric Distribution", "Left-skewed Distribution" or "Right-skewed Distribubtion". Note that the input data should be unimodal and the list can't be empty.

Hi guys, this is a simple code project for my Python class final.
Hope the code can help a little if someone reads it.(Probably not, LOL)


# Calculate the total number of values in the input list.
def count_number(input_list):
    
    counter = 0
    
    for number in input_list:
        counter += 1
    
    return counter

# Calculate the mean of the data in the input list.
def data_mean(input_list):
    
    number_sum = 0
    counter = count_number(input_list)
    
    # Add up all values in input list.
    for number in input_list:
        number_sum += number
        
    # Divide the sum of values by the number of values.
    mean = number_sum / counter

    return mean

# Calculate the median of the data in the input list.
def data_median(input_list):
    
    sorted_list = sorted(input_list)
    counter = count_number(input_list)
    
    # If the number of values in input list is even, the data median is the middle value.
    if counter % 2 == 0:
        median = (input_list[counter // 2 - 1] 
                  + input_list[counter // 2 + 1 - 1]) / 2
    
    # If the number of values in input list is odd, the data median is the average of the middle two values.
    else:
        median = input_list[(counter + 1) // 2 - 1]
    
    return median

# Define count_list as a list.
count_list = []

# Construct a dictionary from input list whose keys are the numbers in input list, and values are the frequency of the numbers.
def dic_list(input_list):
   
    # Use count method to count the frequency of numbers occur in the input list.
    for item in input_list:
        count_list.append(input_list.count(item))
    
    # Use zip and dict method to make the numbers as keys, frequency of numbers as values,
    # to create the dictionary: dic_mode.
    dic_mode = dict(zip(input_list, count_list))

    return dic_mode

# Find the maximized frequency of the number and return the number.
def max_key(dic_mode):
    
    maximum = 0
    
    # Find the number with maximized frequency.
    for item in dic_mode:
        
        if dic_mode.get(item) > maximum:
            maximum = dic_mode.get(item)
            mode = item
    
    return mode 

# Find the mode of data.
def data_mode(input_list):
    
    dic_mode = dic_list(input_list)
    mode = max_key(dic_mode)
    
    return mode

# Find the shape of the distribution of data in input list, based on the relationship among the mean, median and mode of the data.
def shape_dis(input_list):
    
    # Use the functions wrote before to get the mean, median and mode of the data.
    mean = data_mean(input_list)
    median = data_median(input_list)
    mode = data_mode(input_list)
    
    if mean == median == mode:
        shape = 'Symmetric Distribution'
    
    elif mean < median < mode:
        shape = 'Left-skewed Distribution'
    
    else: # mean > median > mode
        shape = 'Right-skewed Distribution'
        
    return shape
