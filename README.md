pytest-rerunfailures
====================

A py.test plugin that re-runs failed tests up to X times to eliminate flakey failures

Installation:
============
    (sudo) pip install git+https://github.com/klrmn/pytest-rerunfailures.git

Parameters:
===========
* --reruns=N    reruns failing tests N times (default 0)
* -r R          reports on which tests were rerun (optional, may be combined with sxXF)

Notes:
======

When teardown fails, two reports are generated for the case, one for the test
case and the other for the teardown error.

In some versions of py.test, when setup fails on a test that has been marked with xfail, 
it gets an XPASS rather than an XFAIL 
(https://bitbucket.org/hpk42/pytest/issue/160/an-exception-thrown-in)
fix should be released in version 2.2.5

Output:
=======
The output should look something like this if run with '--reruns=2 -r fsxXR'

    test_report_on_with_reruns.py .FxXR
    
    =================================== FAILURES ===================================
    ________________________________ test_fake_fail ________________________________
    
        @pytest.mark.nondestructive
        def test_fake_fail():
    >       raise Exception, "OMG! fake test failure!"
    E       Exception: OMG! fake test failure!
    
    test_report_on_with_reruns.py:9: Exception
    =========================== rerun test summary info ============================
    RERUN test_report_on_with_reruns.py::test_flaky_test
    RERUN test_report_on_with_reruns.py::test_flaky_test
    =========================== short test summary info ============================
    FAIL test_report_on_with_reruns.py::test_fake_fail
    XFAIL test_report_on_with_reruns.py::test_xfail
      this will fail
    XPASS test_report_on_with_reruns.py::test_xpass this will pass
    ====== 1 failed, 1 passed, 1 xfailed, 1 xpassed, 1 rerun in 0.04 seconds =======


Compatibility:
==============

While this plugin is compatible with pytest-mozwebqa, the tests for this plugin may not be run with the pytest-mozwebqa plugin installed.

This plugin is *not* compatible with pytest-xdist's --looponfail flag.

This plugin is also not compatible with the core --pdb flag.

Continuous Integration
----------------------
[![Build Status](https://secure.travis-ci.org/klrmn/pytest-rerunfailures.png?branch=master)](http://travis-ci.org/klrmn/pytest-rerunfailures)
