% short code to import .csv world indicators and plot a few comparisons
% Mulugeta Semework, October 28, 2016, New York, NY.

%% open folder browser, import data and collect important variables
files1 = dir([uigetdir '/*.csv']);
FileNames = cell(numel(files1),1);

AllIndicatorData = [];
meanDurMnth = zeros(numel(files1),1);
for f = 1:numel(files1)
    dtTbl = (readtable(files1(f,1).name,'ReadRowNames',false));
    name = [files1(f,1).name(1:end-4)];
    evalc(['AllIndicatorData.' name '= dtTbl;']);
end
%% create relevant data table for full sets

MED = (AllIndicatorData.MentalExpenditure);%mental
cntryGd = table2array(MED(3:end,2));
cntryNms = table2array(MED(3:end,1));

[goodD l]= find(~isnan(cntryGd));
TheGoodTable = zeros(numel(goodD),5);
cntryNms = (cntryNms(goodD));

TheGoodTable(:,1) = (cntryGd(goodD));
%1 mental,'Mental expenditure (% of central government expenditure)'

MilitaryExp = (AllIndicatorData.MilitaryExpenditure);
%2 Military,'Military expenditure (% of central government expenditure)'
GDPG = (AllIndicatorData.GDPGrowth);%3 GDP, 'GDP per capita (current US$)'
EduExp = (AllIndicatorData.EducationExpenditure);
%4 Edu,'Expenditure on education as % of total government expenditure (%)'

for g =1:numel(goodD)
    MeExp = AllIndicatorData.MilitaryExpenditure;
    cRow = strmatch(char(cntryNms(g)),...
        table2array(MilitaryExp(3:end,1)),'exact');
    if ~isempty(cRow)
        TheGoodTable(g,2) = ...
            str2double(table2array(MilitaryExp(cRow+2,56)));
    end
    
    cRow = strmatch(char(cntryNms(g)),table2array(GDPG(3:end,1)),'exact');
    if ~isempty(cRow)
        TheGoodTable(g,3) = str2double(table2array(GDPG(cRow+2,56)));
    end
    
    cRow = strmatch(char(cntryNms(g)),table2array(EduExp(3:end,1)),'exact');
    if ~isempty(cRow)
        TheGoodTable(g,4) = str2double(table2array(EduExp(cRow+2,56)));
    end
end
%% sort by GDP, keep both 
[srtG,srtDRows] = sort(TheGoodTable(:,3),'ascend');
TheGoodTable2 = TheGoodTable(srtDRows,:);
%% figure prep

circleSize5 = 30;
MarkerFaceColor1 = [0 0 1];
MarkerFaceColor2 = [1 0 0];

TheGoodTable2(:,5) = ceil(((TheGoodTable2(:,3)/...
    max(TheGoodTable2(:,3))))*circleSize5);


%%  F    i       g         u        r          e            s
clf,clc
figure(11111),clf,
hfig = gcf;
set(gcf,'Name','World Expenditures')
%%
% GDP, vs military and mental expenditure
axes('Units','normalized','position',[0.1 0.6 0.3 0.35]),cla
% hold on
for g =1:numel(goodD)
    scatter3(TheGoodTable2(g,3),TheGoodTable2(g,2),TheGoodTable2(g,1),'o',...
        'MarkerEdgeColor',MarkerFaceColor1,...
        'MarkerFaceColor',MarkerFaceColor1,'LineWidth',...
        max(1,TheGoodTable2(g,5)))
    hold on %x GDP, y military , z%mental
end
% view(11,23)
maxXandY=max([TheGoodTable2(:,3);TheGoodTable2(:,2);TheGoodTable2(:,1)]);
maxXandY = roundn(maxXandY,3);
xMaxlims = roundn(max(TheGoodTable2(:,3)),2);
yMaxlims = roundn(max(TheGoodTable2(:,2)),1);
zMaxlims = roundn(max(TheGoodTable2(:,1)),1);


set(gca,'XTick',round([0 xMaxlims/2 xMaxlims]),...
    'XTickLabel',round([0 xMaxlims/2 xMaxlims]),...
    'YTick',round([0 yMaxlims/2 yMaxlims]),'YTickLabel',...
    round([0 yMaxlims/2 yMaxlims]),...
    'ZTick',round([0 zMaxlims/2 zMaxlims]),'ZTickLabel',...
    round([0 zMaxlims/2 zMaxlims]),...
    'color',[0.71 0.71 0.7],'xcolor','k','ycolor','k','fontsize',15);


xlabel('GDP per capita (current US$)'),
ylabel({'Military expenditure';'(% gov. exp.)'},'rotation',60)
zlabel({'              Mental health expenditure';....
    '               (% government expenditure)'})
title('GDP vs military and MENTAL health expenditures (world-wide)')
view(11,23)

%% GDP, vs military and Education expenditure
axes('Units','normalized','position',[0.55 0.6 0.3 0.35]),cla

for g =1:numel(goodD)
    scatter3(TheGoodTable2(g,3),TheGoodTable2(g,2),TheGoodTable2(g,4),'o',...
        'MarkerEdgeColor',MarkerFaceColor1,...
        'MarkerFaceColor',MarkerFaceColor1,'LineWidth',...
        max(1,TheGoodTable2(g,5))),hold on %x GDP, y military , z%mental
end
view(11,23)

maxXandY = roundn(max([TheGoodTable2(:,3);...
    TheGoodTable2(:,2);TheGoodTable2(:,1)]),3);

xMaxlims = roundn(max(TheGoodTable2(:,3)),2);
yMaxlims = roundn(max(TheGoodTable2(:,2)),1);
zMaxlims = roundn(max(TheGoodTable2(:,4)),1);
set(gca,'XTick',round([0 xMaxlims/2 xMaxlims]),'XTickLabel',...
    round([0 xMaxlims/2 xMaxlims]),'YTick',round([0 yMaxlims/2 yMaxlims]),...
    'YTickLabel',round([0 yMaxlims/2 yMaxlims]),...
    'ZTick',round([0 zMaxlims/2 zMaxlims]),'ZTickLabel',...
    round([0 zMaxlims/2 zMaxlims]),...
    'color',[0.71 0.71 0.7],'xcolor','k','ycolor','k','fontsize',15);

xlabel('GDP per capita (current US$)'),
ylabel({'Military expenditure';'(% government exp.)'},'rotation',60)
zlabel({'              Education expenditure';...
    '              (% government expenditure)'})
title('GDP vs military and EDUCATION expenditures (world-wide)')
view(11,23)

%% military vs mental expenditure

axes('Units','normalized','position',[0.075 0.1 0.35 0.35]),cla
for g =1:numel(goodD)
    plot(TheGoodTable2(:,1),TheGoodTable2(:,2),'om','MarkerFaceColor',...
        MarkerFaceColor1,'LineWidth',2,'MarkerSize',...
        max(1,TheGoodTable2(g,5))*10)
end

maxXandY = roundn(max([TheGoodTable2(:,2);TheGoodTable2(:,1)]),1);
xlim([0,maxXandY+5]),hold on
ylim([0,maxXandY+5]),hold on
line([0,maxXandY+5],[0,maxXandY+5],'linestyle','--','linewidth',2,...
    'color','r'),hold on
set(gca,'YTick',round([0 maxXandY/2 maxXandY]),'YTickLabel',...
    round([0 maxXandY/2 maxXandY]),'XTick',round([0 maxXandY/2 maxXandY]),...
    'XTickLabel',round([0 maxXandY/2 maxXandY]),...
    'color',[0.1 0.1 0],'xcolor','k','ycolor','k','fontsize',15);
xlabel({'Mental health expenditure';'(% government expenditure)'},...
    'fontsize',15),
ylabel({'Military expenditure';'(% government expenditure)'},'fontsize',15)
title('Military vs mental health expenditures (world-wide)')
axis square


%% military vs education expenditure
axes('Units','normalized','position',[0.525 0.1 0.35 0.35]),cla
for g =1:numel(goodD)
    plot(TheGoodTable2(:,1),TheGoodTable2(:,4),'om','MarkerFaceColor',...
        MarkerFaceColor1,'LineWidth',2,'MarkerSize',...
        max(1,TheGoodTable2(g,5))*10)
end

maxXandY = roundn(max([TheGoodTable2(:,4);TheGoodTable2(:,1)]),1);
xlim([0,maxXandY+5]),hold on
ylim([0,maxXandY+5]),hold on
line([0,maxXandY+5],[0,maxXandY+5],'linestyle','--','linewidth',2,...
    'color','r'),hold on
set(gca,'YTick',round([0 maxXandY/2 maxXandY]),'YTickLabel',...
    round([0 maxXandY/2 maxXandY]),'XTick',round([0 maxXandY/2 maxXandY]),...
    'XTickLabel',round([0 maxXandY/2 maxXandY]),...
    'color',[0.1 0.1 0],'xcolor','k','ycolor','k','fontsize',15);
xlabel({'Education expenditure';'(% government expenditure)'},'fontsize',15)
ylabel({'Military expenditure';'(% government expenditure)'},'fontsize',15)
title('Military vs education expenditures (world-wide)')
axis square

%%
set(gcf,'color','w')
