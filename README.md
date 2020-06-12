# data-distribution
For calculating the mean, median and mode for unimodal data from the input list. Then compare the mean, median and mode to get the shape of the unimodal data distribution. The output (shape of distribution) can be "Symmetric Distribution", "Left-skewed Distribution" or "Right-skewed Distribubtion". Note that the input data should be unimodal and the list can't be empty.

Hi guys, this is a simple code project for my Python class final.
Hope the code can help a little if someone reads it.(Probably not, LOL)

"""A collection of function for doing my project.
"""

def count_number(input_list):
    """Calculate the total number of values in the input list.
    
    Parameters
    ----------
    input_list : list
        List containing all data to analyze.
        
    Returns
    -------
    counter : integer
        The total number of values in the input list. 
    """
    
    counter = 0
    
    for number in input_list:
        counter += 1
    
    return counter


def data_mean(input_list):
    """Calculate the mean of the data in the input list.
    
    Parameters
    ----------
    input_list : list
        List containing all data to analyze.
    number_sum : integer or float
        Sum of all values in input list.
        
    Returns
    -------
    mean : integer or float
        The mean of the data in input list. 
    """
    
    number_sum = 0
    counter = count_number(input_list)
    
    # Add up all values in input list.
    for number in input_list:
        number_sum += number
        
    # Divide the sum of values by the number of values.
    mean = number_sum / counter

    return mean

def data_median(input_list):
    """Calculate the median of the data in the input list.
    
    Parameters
    ----------
    input_list : list
        List containing all data to analyze.
        
    Returns
    -------
    median : integer or float
        The median of the data in input list. 
    """
    
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

def dic_list(input_list):
    """Construct a dictionary from input list whose keys are the numbers in input list,
    and values are the frequency of the numbers.
    
    Parameters
    ----------
    input_list : list
        List containing all data to analyze.
        
    Returns
    -------
    dic_mode : dictionary
        The dictionary whose keys are the numbers in input list,
    and the values are the frequency of the numbers.
    """
    
    # Use count method to count the frequency of numbers occur in the input list.
    for item in input_list:
        count_list.append(input_list.count(item))
    
    # Use zip and dict method to make the numbers as keys, frequency of numbers as values,
    # to create the dictionary: dic_mode.
    dic_mode = dict(zip(input_list, count_list))

    return dic_mode

def max_key(dic_mode):
    """Find the maximized frequency of the number and return the number.
     
    Parameters
    ----------
    dic_mode : dictionary
        Dictionaty containing numbers as keys and frequency of numbers as values.
        
    Returns
    -------
    mode : int or float
        The number whose frequency is the highest in the input list.
    """

    maximum = 0
    
    # Find the number with maximized frequency.
    for item in dic_mode:
        
        if dic_mode.get(item) > maximum:
            maximum = dic_mode.get(item)
            mode = item
    
    return mode 

def data_mode(input_list):
    """Find the mode of data.
     
    Parameters
    ----------
    input_list : list
        List containing all data to analyze.
        
    Returns
    -------
    mode: int or float
        The mode of the data from input list.
    """
    
    dic_mode = dic_list(input_list)
    mode = max_key(dic_mode)
    
    return mode

def shape_dis(input_list):
    """Find the shape of the distribution of data in input list,
    based on the relationship among the mean, median and mode of the data.
     
    Parameters
    ----------
    input_list : list
        List containing all data to analyze.
        
    Returns
    -------
    shape: string
        The shape of the data distribution from input list.
    """
    
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
