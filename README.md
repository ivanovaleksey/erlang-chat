Самый минимум - это erlang-сервер, слушающий tcp порт 1234 к которому могли бы подключаться клиенты вроде telnet/net cat, оптимизировать под миллиард подключений не надо, для тестов достаточно будет 2-10. Сервер слушает что пишут ему клиенты и отправляет написанные сообщения всем прямо сейчас подключенным клиентам. Сообщения разделяются через \n.

Дальнейшие полезные улучшения: 
сообщения при отправке помечать таймстампом и источником, например [hh:mm](ip:port): <message>\n
позволить пользователю написав сообщение setnick <name> выставить себе ник, который будет указан вместо (ip:port)
возможность указать в конфиге (если сильно хочется можно даже в самих исходниках, но главное в месте, где было бы легко поменять) максимальную длину сообщения. Если в сообщении больше чем n символов, то всё, что не влезло заменяется на [cut. message too long]
свежеподключившемуся клиенту выдаётся n сообщений написанных пока его не было.
если в тексте сообщения встречается слово shit или чёрт, то с вероятностью 10% пользователь будет кикнут из чата, а его сообщение не будет отправлено остальным участникам.

Ну и ещё предлагается написать клиент для этого сервера, примерный api:
chat:connect(“localhost”, 1234).
chat:set_nick(“h@ckerZ”).
chat:send(“message”).
chat:get_new(). % печатает сообщения полученные с момента последнего запуска get_new() или сообщение “no messages for you” если ничего ещё не приходило
chat:close().
