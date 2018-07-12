eaoi
=====

   AOI for game.

Build
-----

    $ make all
    
    $ erl -pa ebin
    > eaoi:create(1,1,2560,2560).
    > eaoi:addMon(1,1,{mon,1},pid,10,20,<<"all_attr_mon1">>).
    > eaoi:addMon(1,1,{mon,2},pid,10,21,<<"all_attr_mon2">>).
    > eaoi:moveMon(1,1,{mon,1},pid,10,20,10,19,<<"remove_mon">>,<<"move_mon">>,<<"all_attr_mon1">>).
    > eaoi:updateMon(1,1,{mon,2},pid,10,21,<<"update_mon2">>,<<"all_attr_mon2">>).
    > eaoi:addDrop(1,1,{drop,1},pid,10,20,<<"all_attr_drop1">>).
    > eaoi:addDrop(1,1,{drop,2},pid,10,21,<<"all_attr_drop2">>).
    > eaoi:updateDrop(1,1,{drop,2},pid,10,21,<<"update_drop2">>,<<"all_attr_drop2">>).
    > eaoi:eventMon(1,1,10,20,[{pk,123}]).
    > eaoi:eventDrop(1,1,10,20,[{pk,123}]).
    
    > eaoi:add(1,1,{player,1},node,socket,pid,10,20,<<"all_attr_player1">>).
    > eaoi:add(1,1,{player,2},node,socket,pid,10,21,<<"all_attr_player2">>).
    > eaoi:move(1,1,{player,1},node,socket,pid,10,20,10,21,<<"remove_player1">>,<<"move_player1">>,<<"all_attr_player1">>).
    > eaoi:update(1,1,{player,1},node,socket,pid,10,21,<<"update_player2">>,<<"all_attr_player2">>).
    > eaoi:event(1,1,10,20,[{pk,123}]).
    
    > eaoi:send_by_view(1,1,10,20,<<"hello">>).
    
    
    > eaoi:remove(1,1,{player,2},node,socket,10,21,<<"remove_player2">>).
    > eaoi:removeMon(1,1,{mon,1},10,21,<<"remove_mon">>).
    > eaoi:removeDrop(1,1,{drop,1},10,21,<<"remove_drop">>).
    > eaoi:destroy(1,1).
    
    
    玩家进程需处理事件
    {event,Event_list}            
    
    Mon进程需处理事件
    {event,EventMon_list}
    {ai,Ai_dict}                  Ai_dict --> key:Id value:{Pid,X,Y}  
    
    Drop进程需处理事件
    {event,EventDrop_list}
    
    
    共对外提供 17 个接口
    %% 创建  {ok,Pid} | {error,Reason}
	eaoi:create(Map_id,Copy_id,Map_X,Map_Y).
	%% 销毁 
	eaoi:destroy(Map_id,Copy_id).
    
    %% 九宫格广播
	eaoi:send_by_view(Map_id,Copy_id,X,Y,Packets).
	
	%% 玩家 - 事件
	eaoi:event(Map_id,Copy_id,X,Y,Event_list).
	%% 玩家 - 删
	eaoi:remove(Map_id,Copy_id,Id,Node,Socket,X,Y,Packet_remove).
	%% 玩家 - 增
	eaoi:add(Map_id,Copy_id,Id,Node,Socket,Pid,X,Y,Packets).
	%% 玩家 - 移
	eaoi:move(Map_id,Copy_id,Id,Node,Socket,Pid,O_X,O_Y,X,Y,Packet_remove,Packet_move,Packets).
	%% 玩家 - 改
	eaoi:update(Map_id,Copy_id,Id,Node,Socket,Pid,X,Y,Packet_update,Packets).
	
	%% Mon - 事件
	eaoi:eventMon(Map_id,Copy_id,X,Y,Event_list).
	%% Mon - 删
	eaoi:removeMon(Map_id,Copy_id,Id,X,Y,Packet_remove).
	%% Mon - 增
	eaoi:addMon(Map_id,Copy_id,Id,Pid,X,Y,Packets).
	%% Mon - 移
	eaoi:moveMon(Map_id,Copy_id,Id,Pid,O_X,O_Y,X,Y,Packet_remove,Packet_move,Packets).
	%% Mon - 改
	eaoi:updateMon(Map_id,Copy_id,Id,Pid,X,Y,Packet_update,Packets).
	
	%% Drop - 事件
	eaoi:eventDrop(Map_id,Copy_id,X,Y,Event_list).
	%% Drop - 删
	eaoi:removeDrop(Map_id,Copy_id,Id,X,Y,Packet_remove).
	%% Drop - 增
	eaoi:addDrop(Map_id,Copy_id,Id,Pid,X,Y,Packets).
	%% Drop - 改
	eaoi:updateDrop(Map_id,Copy_id,Id,Pid,X,Y,Packet_update,Packets).
	
	
	
