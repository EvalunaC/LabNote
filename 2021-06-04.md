## 06-04-2021

geo download problem

(myenv) [ychen42@bcmpapl2 ~]$ jupyter nbextension enable --py widgetsnbextension
Enabling notebook extension jupyter-js-widgets/extension...
Traceback (most recent call last):
  File "/extraspace/ychen42/Anaconda3/envs/myenv/bin/jupyter-nbextension", line 10, in <module>
    sys.exit(main())
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/jupyter_core/application.py", line 254, in launch_instance
    return super(JupyterApp, cls).launch_instance(argv=argv, **kwargs)
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/traitlets/config/application.py", line 845, in launch_instance
    app.start()
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/nbextensions.py", line 980, in start
    super().start()
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/jupyter_core/application.py", line 243, in start
    self.subapp.start()
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/nbextensions.py", line 888, in start
    self.toggle_nbextension_python(self.extra_args[0])
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/nbextensions.py", line 861, in toggle_nbextension_python
    return toggle(module,
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/nbextensions.py", line 474, in enable_nbextension_python
    return _set_nbextension_state_python(True, module, user, sys_prefix,
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/nbextensions.py", line 373, in _set_nbextension_state_python
    return [_set_nbextension_state(section=nbext["section"],
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/nbextensions.py", line 373, in <listcomp>
    return [_set_nbextension_state(section=nbext["section"],
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/nbextensions.py", line 343, in _set_nbextension_state
    cm.update(section, {"load_extensions": {require: state}})
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/config_manager.py", line 131, in update
    self.set(section_name, data)
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/config_manager.py", line 108, in set
    self.ensure_config_dir_exists()
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/site-packages/notebook/config_manager.py", line 65, in ensure_config_dir_exists
    os.makedirs(self.config_dir, 0o755)
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/os.py", line 215, in makedirs
    makedirs(head, exist_ok=exist_ok)
  File "/extraspace/ychen42/Anaconda3/envs/myenv/lib/python3.9/os.py", line 225, in makedirs
    mkdir(name, mode)
OSError: [Errno 28] No space left on device: '/home/ychen42/.jupyter'
