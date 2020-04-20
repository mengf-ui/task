# task
task
    def __del__(self):
        while True:
            process_status = False
            for i in self.process_dict:
                if i.is_alive() is True:
                    process_status = True
            if process_status == False:
                break
            time.sleep(5)
        alluredir = BaseConfig.get_conf("Smoke.ini", "pytestLogPath", "alluredir")
        alluredir = alluredir + '\\' + self.now_str
        cmd = "allure serve " + alluredir +' -p 8888'
        subprocess.call(cmd, shell=True)
