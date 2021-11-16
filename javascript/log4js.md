# log4js
---

example:

```js
import Log4js from "log4js";

Log4js.configure({
    appenders: {
      all_in_file: { 
          type: 'file', 
          filename: 'example.log',
        },
      all_stderr : { type: 'stderr' }
    },
    categories: {
      default: { appenders: [ 'all_in_file', 'all_stderr'], level: 'all' }
    }
  });
  
let logger = new Log4js.getLogger("consoleTest");
logger.trace("debug test")
logger.debug("debug test")
logger.info("info test")
logger.warn("warn test")
logger.error("error test")
logger.fatal("error test")
logger.log("error", "test generic log");

```