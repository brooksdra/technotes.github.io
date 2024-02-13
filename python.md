# Python

### Imaging Controller:
    • Review learn solid programming principals Duck Typing to help with RestBuilder type Union[real, simulator]
    • See https://www.linkedin.com/learning/learning-solid-programming-principles/duck-typing?autoSkip=true&autoplay=true&resume=false&u=99855674
    • Did I generate a unit test for the simulator?
    • What is mypy?
    • See dependency inversion principals https://www.linkedin.com/learning/learning-solid-programming-principles/introduction-to-the-dependency-inversion-principle?autoSkip=true&autoplay=true&resume=false&u=99855674
    • Also see dependency inversion principals configuration
    • Watchman: Monitoring Dependency Conflictsfor Python Library Ecosystem 
See https://yepangliu.github.io/files/ICSE2020_Watchman.pdf

### Good article about speeding up the python build:
https://pythonspeed.com/articles/smaller-python-docker-images/

### Print a list of all modules currently running:
`print('\n'.join(sys.modules.keys()))`

Reach into module medtox.rest.rest_builder to read local variable PC_SERVER>IP
`sys.modules['medtox.rest.rest_builder'].PC_SERVER_IP = newVal`
`ExistingVal = sys.modules['medtox.rest.rest_builder'].PC_SERVER_IP`

Use if variable:  over if variable is not None
![python-bool-tidbit.png](images%2Fpython-bool-tidbit.png)

### Class vs. Instance variables
    class CSStudent:
        stream = 'cse'                     # Class Variable
        def __init__(self,name,roll):
            self.name = name            # Instance Variable
            self.roll = roll            # Instance Variable

### Trapping multiple exceptions: 
    # Note exceptions can be provided programmatically
    try:
      led_config_loader = LedConfigLoader(filename)
      assert False
    except exceptions[i] as expected:
      print(expected)
      assert True
    except Exception as unknown:
      print(unknown)
      assert False

### Unit Test Mocking
An interesting reference to pytest fixtures
https://levelup.gitconnected.com/a-comprehensive-guide-to-pytest-3676f05df5a0

    Mock 'requests.post' method's return value and/or initiate a side effect of calling this method. (I.e. throw an exception. You can eliminate either or pass none as they are mutually exclusive)
    mocker.patch(
       'requests.post',
       return_value=RestBuilder.HTTP_RESPONSE_OK,   # HTTP_RESPONSE_OK from the request post
       side_effect=Exception('Straight Exception')  # When an exception is thrown
    )

### A good way to count the number of calls to a method is by using pytest.mocker
`mock_logger_info = mocker.patch.object(logging.Logger, 'info')`
`assert mock_logger_info.call_count == expected_log_counts`
Also see C:\ProtedyneSuite\charm-medtox-dev\ImagingSubsystem\tests\commons\hardware\leds\led_controller_test.py

### Mock complete method calls of the internal logger, in this case to count method calls.
`log_info_count = 0;`  
`mocker.patch.object(logging.Logger, 'info', new=log_info_tick)`

### arg1 and arg2 are required by the OG logging.Logger.info method. So you can use them
### arg1 is calling source information, arg2 is the log message
    def log_info_tick(arg1, arg2):
        global log_info_count
        log_info_count+= 1

### A Capsys is built into PyTest for access to stdin/stdout
    def test_print(capsys):
        print('hello')
        captured = capsys.readouterr()
        assert 'hello' in captured.out
        print('world')
        captured = capsys.readouterr()
        assert 'world' in captured.out

### Getting the call list from a mock object, all method calls to that object (optionally in order)
      calls = [
          call(channels[channel].endpoint_period, 'w'),
          call().write('{written}'.format(written=written_value)),
          call().flush(),
          call().close()
      ]
      mock_sys_fs = mock_open()
      with patch('builtins.open', mock_sys_fs):
      # Act        
      channels[channel].set_period(written_value)
      # Assert 
      mock_sys_fs.assert_has_calls(calls, True)
      assert channels[channel].config.period == written_value


### Unit Testing for exceptions is a matter of wrapping the test in a try catch
    try:
      led_config_loader= LedConfigLoader(filename)
      assert False
    except exceptions[i] as expected:
      assert 
    Trueexcept Exception as unknown:
      assert False

### Fake file input data:
    with patch(
      'builtins.open',
      new=mock_open(read_data=file_contents[i])
    ) as read_file:
    # This is indented as it is used withing the with patch.
    led_config_loader = LedConfigLoader(filename)
